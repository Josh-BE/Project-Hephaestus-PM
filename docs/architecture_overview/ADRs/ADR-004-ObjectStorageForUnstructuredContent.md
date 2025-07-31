# ADR 004: Object Storage for Unstructured Content

## 1. Context

Project Hephaestus's core operations involve the ingestion, processing, and generation of vast quantities of unstructured and semi-structured data. This includes:

- Raw educational source materials (e.g., PDFs, articles, research papers, videos).
    
- Intermediate AI processing outputs (e.g., large text chunks, embeddings, temporary files).
    
- AI-generated learning content (e.g., long-form explanations, analogies, scenario descriptions).
    
- Potential future multimedia assets (e.g., images, audio snippets for Tier 4 visuals).
    

Managing this data efficiently and cost-effectively, especially with a vision to serve billions of users and support petabytes of data, is crucial. Storing such large volumes directly within our primary relational database (PostgreSQL) would significantly degrade its performance, inflate costs, and complicate its core purpose of managing structured metadata and transactional data.

## 2. Decision

The decision is to **utilize cloud object storage services** (e.g., AWS S3, Google Cloud Storage, Azure Blob Storage, or Supabase Storage) as the primary repository for all unstructured content within Project Hephaestus. Structured metadata and references to these objects (e.g., file paths, IDs, versioning information) will be stored in PostgreSQL.

## 3. Alternatives Considered

- **Storing Large Binary Objects (BLOBs/TEXT) Directly in PostgreSQL:**
    
    - Pros: Single database for all data, simpler initial setup if data volume is tiny.
        
    - Cons: Dramatically increases database size and backup/restore times; severely degrades query performance for relational data; much higher storage cost per GB compared to object storage; not designed for efficient storage or retrieval of large files.
        
- **Network File Systems (NFS) or Block Storage on VMs:**
    
    - Pros: Familiar filesystem interface; good for certain legacy applications.
        
    - Cons: Requires provisioning and managing virtual machines, storage volumes, and network file shares; introduces significant operational overhead (patching, scaling, backups) that contradicts our serverless-first strategy; less inherently scalable and resilient than cloud object storage.
        
- **Dedicated NoSQL Document Stores for Large Texts:**
    
    - Pros: Good for semi-structured data, high read/write throughput for specific use cases.
        
    - Cons: Still potentially more expensive than object storage for pure binary/text blobs; might introduce additional complexity if not perfectly aligned with data access patterns (e.g., if primarily used for large file storage rather than document querying).
        

## 4. Consequences (Pros & Cons of the Decision)

### 4.1. Positive Consequences (Why Object Storage Aligns with Our Vision)

- **Extreme Scalability:** Cloud object storage is virtually limitless and designed to store petabytes of data without requiring manual scaling efforts. This directly supports our "Infinite Scalability by Design" tenet for billions of users.
    
- **Cost-Effectiveness:** Offers significantly lower storage cost per GB compared to relational databases or block storage, making it highly economical for vast amounts of data.
    
- **High Availability & Durability:** Built-in redundancy and replication across multiple availability zones ensures extremely high data durability and availability, minimizing data loss risk.
    
- **Operational Simplicity:** As a fully managed service, it requires no server management, patching, or scaling from the development team, directly supporting our "Radical Automation & Leverage" for a solo technologist.
    
- **Optimized for Large Files & AI Needs:** Efficiently handles large objects (documents, videos) and can be directly accessed by serverless functions or AI inference engines without impacting database performance.
    
- **Clear Data Segregation:** Maintains PostgreSQL's performance for structured, transactional data by offloading large, unstructured content to its specialized storage solution.
    

### 4.2. Negative Consequences (Challenges & Mitigations)

- **Eventual Consistency (Mitigated for Critical Paths):** Object storage typically offers eventual consistency, meaning a newly written object might not be immediately readable across all replicas.
    
    - Mitigation: For critical paths (e.g., a newly generated course module), ensure read-after-write consistency guarantees are checked or implement compensatory logic (e.g., retry mechanisms). For most learning content, eventual consistency is acceptable.
        
- **Direct Querying Limitations:** Cannot directly query content within objects (e.g., search for a specific word inside a PDF stored as an object).
    
    - Mitigation: This is handled by processing the content for metadata and text extraction (e.g., indexing text into a search engine or vector database), which is then stored in PostgreSQL or other specialized search services.
        
- **Access Patterns vs. Costs:** While overall cheap, frequent access to many small objects or very high transfer rates can accumulate costs.
    
    - Mitigation: Optimize data retrieval patterns, leverage caching where appropriate, and monitor egress costs. Structure objects logically to minimize redundant retrievals.
        

## 5. Status

Accepted. The strategic adoption of cloud object storage is critical for handling Project Hephaestus's large-scale unstructured data needs, ensuring cost-effective, highly scalable, and operationally simple storage solutions aligned with our vision.