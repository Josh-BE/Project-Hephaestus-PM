### **Product Requirements Document (PRD): Project Hephaestus - Guided Problem Solving** 

### **1. Overview**

This document outlines the product requirements for Project Hephaestus's Guided Problem Solving feature. This feature serves as the crucial bridge between theoretical knowledge and practical competence, enabling learners to apply their understanding in realistic, scenario-based contexts. It represents the pinnacle of our pedagogical approach, fostering true application skills that are directly transferable to real-world challenges.

### **2. Introduction: The Problem We're Solving**

A pervasive gap exists between knowing theoretical concepts and genuinely being able to apply them to solve practical problems. Traditional learning often leaves learners with abstract knowledge but without the necessary experience to navigate real-world complexity, leading to a lack of confidence and competence. This feature addresses this by:

- Providing a safe, simulated environment for learners to apply theoretical knowledge to practical situations.
    
- Enabling the development of problem-solving skills that are crucial for professional success.
    
- Building user confidence by demonstrating their ability to utilize concepts effectively.
    

The primary value proposition this feature offers to the user is a high-quality, free, and incredibly time-efficient/effective method for retaining and actively using learned information, ensuring they gain true, applicable competence.

### **3. Strategic Goals**

As part of the larger Project Hephaestus initiative, the Guided Problem Solving feature aims to:

- **Primary Goal:** Enable learners to consistently apply theoretical knowledge to solve practical problems, thereby building demonstrable competence.
    
- **Engagement Goal:** Drive deeper engagement within the platform by providing a compelling, interactive learning experience that goes beyond passive content consumption.
    
- **Efficacy Goal:** Serve as a core component in proving the platform's educational effectiveness by moving learners from theory to application.
    

(Specific, measurable success metrics for this feature will be defined and tracked in the project's overall KPI dashboard, in alignment with the broader goals of Project Hephaestus.)

### **4. Key Assumptions**

Before proceeding, we are making the following key assumptions. These will be validated through user testing and data analysis post-launch.

- **User Motivation:** We assume users are motivated to move beyond theoretical knowledge and will see value in a feature that requires active effort and critical thinking.
    
- **Engagement Loop Value:** We assume that users will find the iterative "Guided Refinement Loop" to be a valuable learning process and will not perceive it as frustrating or tedious.
    
- **Metric Perception:** We assume that the "Conceptual Accuracy" score will be perceived by users as a helpful and motivating indicator of their understanding, rather than a punitive grade.
    
- **AI Trust:** We assume users will generally trust the AI's feedback and guidance, provided it is encouraging, constructive, and helpful.
    

### **5. User Experience, Flow, and Design**

#### **5.1. Key User Stories**

- **As a learner, I want to** practice applying concepts from my personalized path in realistic, small-scale problems to solidify my understanding.
    
- **As a learner, I want to** receive immediate, specific feedback on my solution attempts so I can understand errors in my application and refine my approach.
    
- **As a learner, I want to** have hints or step-by-step guidance available if I'm stuck on a problem so that I can learn how to approach it without being given the direct answer.
    
- **As a learner, I want to** feel more confident in my skills for real-world encounters and projects after successfully solving these problems.
    

#### **5.2. High-Level User Flow**

1. **Problem Introduction:** The user is presented with a problem-solving scenario dynamically generated based on their current learning path. The scenario includes clear context and a defined task.
    
2. **Solution Attempt:** The user provides a free-form text response (up to 1,500 characters).
    
3. **AI Evaluation & Initial Feedback:** The system evaluates the solution against a predefined rubric, providing targeted feedback and a "Conceptual Accuracy" score (e.g., 8/10).
    
4. **Guided Refinement Loop (Iterative):**
    
    - If the score is below the passing threshold (e.g., < 8/10) or the user requests help, the system offers progressive hints.
        
    - The user revises their solution and resubmits. This loop continues until a passing score is achieved or the user requests the solution.
        
    - **Failure Path:** After four (4) unsuccessful attempts, the system proactively offers to reveal the solution and a detailed explanation.
        
    - **Escape Hatch:** A "Show me the answer" button is always visible.
        
5. **Solution Review & Reinforcement:** Upon completion, the system presents an optimal solution, contrasting it with the user's final attempt to reinforce key concepts.
    
6. **Mastery Update & Next Steps:** The user's Mastery Rubric is updated, and the system recommends the next step.
    

#### **5.3. Wireframes & Design**

(Link to Figma/Miro board with low-fidelity wireframes and high-level mockups will be added here.)

**Note:** Visual designs are critical for conveying the user journey, including the presentation of the problem, the feedback interface, the hint mechanism, and the final solution review screen. These will be developed in parallel with the technical spike.

---

### **6. High-Level Functional Requirements**

#### **6.1. Dynamic Scenario Generation**

The system must generate unique, realistic scenarios for any given concept.

- **Inputs for Generation:**
    
    - **Core Concept(s):** Sourced directly from the user's Personalized Learning Path (e.g., "separation of concerns," "stakeholder management").
        
    - **Difficulty Level:** An initial difficulty setting (e.g., Easy, Medium, Hard) that dictates the complexity of the scenario and the number of confounding variables.
        
    - **Contextual Wrapper:** A randomized but plausible industry or domain (e.g., "a tech startup," "a non-profit," "a retail company") to ground the scenario.
        
- **Generation Constraints & Quality Control:**
    
    - **Solvability Checks:** The generation prompt will require the AI to produce not only the problem but also a model solution and the key rubric items. This ensures the problem is solvable from the outset.
        
    - **Uniqueness Parameters:** The system will use templating combined with dynamic elements to avoid verbatim repetition of problems.
        
    - **Human-in-the-Loop:** For launch (V1), a "Golden Set" of 200+ problems for the most critical learning paths will be pre-generated and vetted by subject matter experts to guarantee a high-quality initial user experience.
        

#### **6.2. Flexible Input Evaluation**

- The system must accept and evaluate free-form text inputs (English only for V1) up to 1,500 characters.
    
- Evaluation of code, file uploads, or other formats is **out of scope for V1**.
    
- The evaluation must score against a rubric of key concepts, allowing for variations in phrasing ("gist" understanding).
    

#### **6.3. Intelligent Hinting & Guidance**

The system must provide multi-level, adaptive hints as detailed in the AI Behavioral Requirements.

#### **6.4. Link to Mastery Tracking**

Successful completion of scenarios must update the user's progress against the Mastery Rubric.

### **7. AI Behavioral Requirements (The "Magic Box" De-risked)**

- **Evaluation Criteria:** "Correctness" will be evaluated against a dynamically generated rubric of 3-5 key concepts. The "Conceptual Accuracy" score (out of 10) will be determined by the percentage of rubric items correctly addressed.
    
- **Feedback Tone & Style:** The AI's persona will be encouraging, Socratic, and pedagogical, guiding users with questions rather than declarative judgments. The tone must never be condescending.
    
- **Hinting Strategy (Progressive Disclosure):**
    
    - **Hint 1:** A general Socratic question to prompt rethinking.
        
    - **Hint 2:** A more direct pointer towards a weakness in the previous answer.
        
    - **Hint 3:** A direct piece of information or a sentence-starter.
        
- **Failure & Feedback Handling:** Every piece of AI-generated feedback must be accompanied by a "Was this feedback helpful? (Yes/No)" widget. This data will be logged for continuous model improvement.
    

---

### **8. Risks, Dependencies, & Mitigations**

- **Dependency:** Functionality of the core AI content generation engine (PRD: Interactive Content Generation).
    
- **Dependency:** Integration with the Personalized Learning Paths engine (PRD: Personalized Learning Paths).
    
- **Dependency:** Reliable external LLM APIs (ADR 003).
    

|   |   |   |
|---|---|---|
|**Risk**|**Level**|**Mitigation Strategy**|
|**LLM Evaluation Inaccuracy**|**High**|A **technical spike/Proof-of-Concept** will be executed before full development. This will test three distinct LLM prompting strategies on a golden set of 100 sample user responses. We will define an acceptable **accuracy threshold of 90%** (AI evaluation matches human expert evaluation) before proceeding.|
|**Inconsistent Problem Quality**|**Medium**|For V1 launch, we will rely on a **pre-generated and human-vetted "Golden Set"** of 200+ problems for core concepts. We will also implement a user-facing **"Report this problem" flag**. All flagged problems will be reviewed to refine the generation prompts for future iterations.|

### **9. Phased Rollout & Release Criteria**

This feature will be rolled out in phases to ensure stability and gather user feedback.

- **Phase 1: Internal Alpha**
    
    - **Audience:** Internal team members.
        
    - **Goal:** Validate core functionality, test integration with learning paths, and identify major bugs.
        
    - **Criteria:** The technical spike for LLM evaluation must be complete with a chosen strategy. The "Golden Set" of human-vetted problems must be loaded.
        
- **Phase 2: Closed Beta**
    
    - **Audience:** A select group of 100-200 power users.
        
    - **Goal:** Gather qualitative feedback on the user experience, hint quality, and perceived value. Monitor success metrics.
        
    - **Criteria:** Core user flow is stable. The "Was this feedback helpful?" mechanism is fully functional and logging data.
        
- **V1 Public Launch (GA)**
    
    - **Goal:** Make the feature available to all users.
        
    - **Release Criteria:**
        
        1. No P0/P1 bugs identified in the Closed Beta.
            
        2. The "Scenario Success Rate" in the beta is at or above a predefined threshold (e.g., 60%).
            
        3. The feedback loop for reporting problems and evaluating hints is fully operational.
            
        4. Legal and privacy reviews are complete.
            

### **10. Out of Scope (for V1)**

- Full, complex project development environments or IDEs.
    
- Multi-user collaborative problem-solving features.
    
- Evaluation of solutions involving external tools, code execution, or physical interactions.
    
- Detailed specifications of the AI algorithms beyond their required behavior.