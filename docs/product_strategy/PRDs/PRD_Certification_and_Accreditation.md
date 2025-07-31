### **PRD: Certification and Accreditation v1.0 (MVP)**

### **1. Overview**

This document outlines the product requirements for the Minimum Viable Product (MVP) of the Certification and Accreditation feature. This feature is crucial for establishing Project Hephaestus as a trusted learning utility by providing learners with verifiable proof of their skills. The primary goal of this MVP is to launch a foundational, secure, and trustworthy certification system to validate our core hypothesis: that employers and learners will value verifiable, skill-based credentials issued by our platform.

### **2. Introduction: The Problem We're Solving**

In today's job market, employers struggle to verify the specific, applicable skills of candidates, while learners lack formal proof of their mastery gained outside traditional degrees. This disconnect hinders talent acquisition and career advancement.

Certification and Accreditation addresses this by providing verifiable, trusted credentials that attest to a learner's mastery of specific skills. **The MVP value proposition is to deliver a trustworthy guarantee of competence for a core set of skills, validating the credential's value with learners and employers before expanding its scope and complexity.**

### **3. V1.0 (MVP) Goals & Key Results (OKRs)**

*   **Objective 1: Validate the core value proposition that verifiable credentials drive learner and employer value.**
    *   **KR1:** Achieve a **15% certification completion rate** among eligible learners within 6 months of launch.
    *   **KR2:** See at least **30% of issued credentials shared** (e.g., to LinkedIn) by learners within 3 months of issuance.
    *   **KR3:** Achieve a learner-reported **Net Promoter Score (NPS) of +20** for the certification feature.

*   **Objective 2: Establish a foundational level of trust and credibility in Project Hephaestus certifications.**
    *   **KR1:** Secure **3-5 employer partners** to participate in a pilot program to review and recognize the credentials.
    *   **KR2:** Ensure the **external verification rate is at least 5%** of all shared credentials within the first quarter.
    *   **KR3:** Maintain a **less than 1% reported rate of integrity issues** or cheating suspicions from our pilot employer partners.

### **4. User Stories for V1.0 (MVP)**

#### **4.1. Learner Experience**
*   As a learner, I want to see a clear list of available certifications and understand the specific learning paths and final assessment required to earn one.
*   As a learner, I want to be notified when I am eligible to take the final certification assessment after completing all prerequisites.
*   As a learner, I want to take a timed, cumulative assessment composed of randomized questions and scenarios to prove my mastery.
*   As a learner, upon passing the assessment, I want to be issued a verifiable digital credential through a recognized third-party platform (e.g., Credly).
*   As a learner, I want to easily add my credential to my LinkedIn profile or share it via a unique URL.
*   As a learner who has failed an assessment, I want to understand my general areas of weakness (without revealing specific answers) and know the policy for retaking the test.

#### **4.2. Employer / Verifier Experience**
*   As an employer, I want to click on a badge or link (e.g., on a candidate's LinkedIn) and be taken to a trusted verification page.
*   As an employer, on the verification page, I want to see the earner's name, the specific skill certified, the date of issuance, and a description of what the credential represents, so I can trust its authenticity.

### **5. V1.0 User Flow (with Failure States)**

1.  **Discovery:** Learner explores the "Certifications" tab in their profile.
2.  **Enrollment & Progress:** Learner pursues a learning path. The UI clearly shows prerequisite modules and their completion status.
3.  **Assessment Readiness:** Upon completing all prerequisites, the "Take Final Assessment" CTA becomes active.
4.  **Assessment Initiation:** User is presented with the rules: it is timed, cumulative, and subject to integrity checks (e.g., single tab focus). User consents and begins.
5.  **Assessment & Evaluation:** The system administers the timed assessment. Upon completion, it is auto-graded.
6.  **Outcome:**
    *   **PASS:** User sees a "Congratulations" screen. A "Claim Your Credential" button initiates the issuance flow via our integrated third-party service.
    *   **FAIL:** User sees a "Try Again" screen. It displays general feedback (e.g., "You showed weakness in scenario-based problem solving") and outlines the **Retake Policy (e.g., a 14-day waiting period)**.
7.  **Credential Issuance & Sharing:** Upon claiming, the user is directed to the third-party platform (Credly) to accept their badge and can use that platform's native sharing tools.
8.  **Verification:** An external party clicks the shared badge/URL, which resolves to the public, trusted verification page hosted by the third-party service.

### **6. V1.0 (MVP) Functional Requirements**

| Category | Requirement | Priority |
| :--- | :--- | :--- |
| **Admin & Setup** | The system must allow an Admin to define a certification by linking it to a specific set of required learning modules and Mastery Rubrics. | **Must-Have** |
| **Assessment** | The assessment must pull from a pre-defined bank of questions and Tier-4 style scenarios, randomized for each user session. | **Must-Have** |
| | The assessment must be strictly timed, auto-submitting when the timer expires. | **Must-Have** |
| **Integrity Checks** | The system must incorporate basic browser-level integrity checks, such as detecting when a user navigates away from the assessment tab and logging these events. | **Must-Have** |
| **Credential Issuance** | The system must integrate via API with a reputable third-party credentialing service **(Decision: Credly/Accredible)** to issue Open Badges. We will **not** build a proprietary credentialing or blockchain solution for V1. | **Must-Have** |
| **Verification** | Verification of credentials will be handled by the third-party service's public portal. Our responsibility is to ensure the correct data is passed to them. | **Must-Have** |
| **User Interface** | A dedicated UI section must exist to show users available certifications, their progress, and post-assessment results/actions. | **Must-Have** |
| **Retake Policy** | The system must enforce a 14-day waiting period for learners who fail an assessment before they can attempt it again. This is configurable by an Admin. | **Must-Have** |

### **7. Phased Rollout / Future Scope (Post-MVP)**

*   **V1.1 (Fast Follow):**
    *   Deeper analytics on assessment performance to inform content improvements.
    *   Partnerships with specific companies to co-create and endorse certifications.
*   **V2.0 (Major Release):**
    *   **Advanced Integrity (POC Required):** Begin R&D on AI-powered integrity monitoring, including the voice-to-text Q&A concept as a proof-of-concept.
    *   Tiered certifications (e.g., "Advanced AI Mastery").
    *   Exploring direct integration with Applicant Tracking Systems (ATS).
*   **Out of Scope for Foreseeable Future:**
    *   Direct university credit transfer.
    *   In-person or human proctoring.
    *   Paper-based certificates.

### **8. Risks & Mitigation**

| Risk | Likelihood | Impact | Mitigation Strategy |
| :--- | :--- | :--- | :--- |
| **Market Value Risk:** Employers may not trust or value a new, unproven credential. | High | High | **Co-develop and pilot the V1 with 3-5 friendly employer partners.** Gather their feedback on the perceived value and trustworthiness to iterate quickly. |
| **Integrity Risk:** Cheating devalues the credential for everyone. | Medium | High | **V1 will not solve all cheating.** We will mitigate by using standard measures (timing, randomization, tab-switching detection) and analyzing assessment data for abnormal patterns. The high-stakes, scenario-based questions are inherently harder to cheat on than simple multiple-choice. |
| **Technical Risk:** Integration with the third-party credentialing service proves more complex than anticipated. | Low | Medium | **Conduct a technical spike/investigation** of the APIs for our top 2 choices (Credly, Accredible) *before* sprint planning begins to de-risk the implementation. |

### **9. Dependencies**

*   **Finalized Content:** A complete question and scenario bank for the first 2-3 certifications must be ready before engineering begins. (Dependency: Content/Learning Team).
*   **Production Ready Services:** Fully functional Performance Assessment Engine and User Progress Analytics services.
*   **Legal/Privacy:** Terms of Service must be updated to include consent for data sharing with the third-party credentialing service and for integrity monitoring.