### **PRD: Personalized Learning Paths**

**1. Overview**

This document outlines the product requirements for the Personalized Learning Paths feature, codenamed Project Hephaestus. This feature is central to our mission of democratizing mastery. It moves beyond static curricula to dynamically adapt content and progression to each individual learner. This PRD defines specific functional and non-functional requirements for a phased rollout, focusing on delivering iterative, data-driven value.

**2. Introduction: The Problem We're Solving**

Traditional learning experiences force diverse learners through identical curricula at a uniform pace, leading to frustration, disengagement, and inefficient use of study time. Students frequently encounter content that is either too basic or too advanced, struggle to connect disparate topics, or feel lost without a clear, individualized roadmap.

Personalized Learning Paths address this by:

- Eliminating the "one-size-fits-all" limitation inherent in conventional education.
    
- Providing a clear, optimized trajectory for learners to achieve specific mastery goals.
    
- Maximizing learning efficiency by focusing on relevant content and addressing individual knowledge gaps.
    

**3. Goals & Success Metrics**

The primary goal is to enable users to embark on a dynamically adapting learning journey that is tailored to their unique needs and learning pace.

|   |   |   |
|---|---|---|
|Metric|V1 (MVP) Target (End of Q1)|V2 Target (End of Q3)|
|**User Engagement**|40% of new users exposed to the feature start a learning path.|60% of new users exposed to the feature start a path; 25% weekly active use by path users.|
|**Learning Efficiency**|Establish baseline time-to-mastery for 3 core concepts.|Reduce baseline time-to-mastery by 15%.|
|**Core Value & Satisfaction**|Achieve a user satisfaction score of 3.5/5.0 on path relevance.|Achieve a score of 4.2/5.0; 30% of users experience one adaptive event.|
|**Path Completion Rate**|10% of started paths are completed.|25% of started paths are completed.|

**3.1. Measurement Protocols**

- **New User Exposure:** A "new user" is any registered user who has not previously started a learning path. They are considered "exposed" if the UI element for starting a path is rendered in their view.
    
- **Time-to-Mastery:** Calculated as the delta between the timestamp of the first module interaction and the timestamp of the successful completion of the final path assessment. Inactivity periods greater than 72 continuous hours will be subtracted from the total time to reflect active learning time.
    
- **User Satisfaction:** Measured via a mandatory 1-5 star rating modal presented once, immediately upon path completion. The prompt will be: "How relevant was this learning path to your goal?"
    
- **Adaptive Event:** An "adaptive event" is logged any time the system automatically adds, removes, or suggests skipping a module based on user performance (see FR-2.1).
    

**4. Phased Rollout Plan**

This feature will be delivered in two distinct phases to manage complexity and accelerate time-to-value.

- **V1: The Foundational Path (MVP):** Focus is to prove that users will define a goal and follow a system-generated path. Functionality includes goal selection, an initial diagnostic, and generation of a static, personalized path with progress tracking. No dynamic adaptation.
    
- **V2: The Dynamic Journey:** Focus is to introduce the "magic" of real-time adaptation. Builds on V1 by introducing dynamic path adjustments based on user performance, user controls for overriding the path, and handling for complex edge cases.
    

**5. User Stories**

**5.1. V1 Stories:**

- As a new learner (Alex), I want to choose my learning goal (e.g., "master Python for data science") from a predefined list so the system can create an initial path for me.
    
- As a new learner (Maya), I want to take a short diagnostic quiz so the system understands my current knowledge and doesn't make me start from scratch.
    
- As a learner, I want to see my entire learning path visualized as a sequence of modules so I know what's coming next.
    
- As a learner, I want to clearly see which modules I have completed so I feel a sense of progress.
    

**5.2. V2 Stories:**

- As a learner who is struggling, I want my learning path to automatically suggest a remedial module when I fail a quiz so I can fill my knowledge gap.
    
- As an advanced learner, I want my path to let me skip a module if I pass a "test-out" assessment so I don't waste time on things I already know.
    
- As a curious learner, I want to manually add an optional, related module to my path so I can explore a topic more deeply without losing my place.
    
- As a learner in a hurry, I want to be able to remove optional modules from my path to focus only on the core concepts required for my goal.
    

**5.3. Edge Case & Negative Stories:**

- As a cautious learner, I want to manually un-complete a module the system skipped for me via the diagnostic, because I want a refresher anyway.
    
- As a frustrated learner, when I fail the same quiz twice, I want to be offered an alternative content format (like a video or article) so I can try a different approach.
    
- As a busy learner, I want my exact place in the path saved automatically so I can close my browser and resume seamlessly later.
    

**6. Functional Requirements**

**6.1. V1: Foundational Path (MVP)**

- **FR-1.1 (Goal Selection):** The system MUST present users with a list of selectable, predefined learning goals.
    
- **FR-1.2 (Diagnostic Assessment):** Upon path creation, the system MUST offer a skippable diagnostic quiz (max 15 questions). Each question MUST be mapped to one or more concept_ids in the content database.
    
- **FR-1.3 (Initial Path Generation):** The system MUST generate a path within 5 seconds of goal selection/diagnostic completion.
    
- **FR-1.4 (Path Content):** The path MUST be an ordered sequence of content modules. If the diagnostic was taken, and a user correctly answers all questions associated with a given concept_id, the corresponding module(s) MUST be marked as "pre-completed."
    
- **FR-1.5 (Path Visualization):** The UI MUST display the path as a clear, linear progression, visually differentiating between completed, current, and upcoming modules.
    

**6.2. V2: The Dynamic Journey**

- **FR-2.1 (Adaptive Logic):** The system MUST adjust the path based on the rules below. All adjustments must be clearly communicated to the user.
    

|   |   |   |
|---|---|---|
|Trigger|Rule|User Experience|
|**Performance: Quiz Critical Failure (Score < 40%)**|Insert the primary remedial module mapped to the concept_id with the most failed questions. Mark the original module as "locked" until the remedial is complete.|Modal: "Looks like this topic was tricky. We've added a review module, '[Remedial Module Name],' to help you master it before moving on." [OK]|
|**Performance: Quiz Struggling (Score 40-65%)**|Make the next module a "Consolidation" module (e.g., extra practice problems) for the failed concept_id optional.|Toast: "Nice try. We've added an optional practice module to help solidify this concept. Feel free to try it or continue."|
|**Performance: Quiz Excellence (Score > 95%)**|If the next 1-2 modules are foundational to the aced concept, mark them as "optional."|Toast: "Great job! Based on your score, the next module '[Module Name]' is now optional. You can complete it or skip ahead."|
|**Behavior: Repeated Failure**|If a user fails the quiz for the same module twice.|Modal: "This concept can be tough. Would you like to try a different approach? [Watch a Video] or [Read an Article]". The system logs a stuck_user event for analysis.|

- **FR-2.2 (Edge Case: Path Override):** Users MUST be able to manually interact with their path:
    
    - **Skip Ahead:** Users can click any "unlocked" module to jump to it, triggering a confirmation modal.
        
    - **Revisit:** Users can click any "completed" module to review it without losing their current place.
        
    - **Override Pre-completion:** Users can click a "pre-completed" module to move it back to the "to-do" state.
        
- **FR-2.3 (Edge Case: Goal Mastery):** If the diagnostic indicates >90% mastery, the system MUST NOT generate a path, instead displaying a congratulatory message and suggesting a more advanced goal.
    

**7. Non-Functional Requirements (NFRs)**

- **NFR-1 (Performance):** Initial path generation ≤ 5s. Adaptive adjustments reflected in UI ≤ 2s.
    
- **NFR-2 (Scalability):** System must support 1,000 concurrent users interacting with paths with ≤ 10% degradation in performance NFRs.
    
- **NFR-3 (Accessibility):** All UI elements MUST be compliant with WCAG 2.1 Level AA.
    
- **NFR-4 (Data Integrity):** User path state changes (completion, adjustments) MUST be successfully committed to the database before the UI update is rendered to the user to prevent data/UI desynchronization.
    

**8. Dependencies & Risks**

|   |   |   |   |
|---|---|---|---|
|ID|Type|Description|Mitigation Strategy|
|**D-1**|Dependency|**AI Content Engine:** Engine for generating/serving content modules.|**Requirement for AI Team:** Provide a stable API endpoint for content retrieval. <br> **Required API Contract:** <br> • **Endpoint:** GET /api/v1/content/module/{module_id} <br> • **Response (Success):** 200 OK { "module_id": "...", "content_type": "...", "data": "..." } <br> • **Response (Error):** 404 Not Found { "error": "Module not found" }|
|**D-2**|Dependency|**Assessment Engine:** Engine for administering quizzes and returning scores.|**Requirement for Assessment Team:** Provide a stable API endpoint for scoring. <br> **Required API Contract:** <br> • **Endpoint:** POST /api/v1/assessment/score <br> • **Request Body:** { "user_id": "...", "quiz_id": "...", "answers": [...] } <br> • **Response (Success):** 200 OK { "score": 85, "correct_array": [...], "failed_concept_ids": [...] }|
|**R-1**|Risk|**Pedagogical Ineffectiveness:** The adaptive logic (FR-2.1) annoys users or harms learning outcomes.|**Mitigation:** In V2, A/B test the adaptive logic against a V1-style static path control group. Closely monitor satisfaction and completion rates. <br> **Reversion Plan:** If the adaptive cohort shows a statistically significant (>5%) decrease in path completion or satisfaction over a 14-day period, the adaptive logic will be remotely disabled for all users via a feature flag, reverting them to the static path experience while the rules are re-evaluated.|
|**R-2**|Risk|**Insufficient User Input:** Users skip the diagnostic, providing no personalization signal.|**Fallback Behavior (FR-1.2):** If a user skips the diagnostic, the system will generate a default, complete path for their chosen goal, assuming zero prior knowledge. This ensures no user is blocked from starting a path.|

**9. Out of Scope**

- Detailed specifications of the AI algorithms for path generation.
    
- Specific UI/UX wireframes or visual designs (handled in separate design artifacts).
    
- Offline learning capabilities.
    
- Multi-user/group-based personalized learning paths.
    
- User-created goals or fully custom path creation (Post-V2).
    
- Integration with third-party content providers.