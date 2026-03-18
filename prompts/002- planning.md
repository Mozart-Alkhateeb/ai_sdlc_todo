Your context is a final requirements file #file:002- final_requirements.md 
**Your Task:** Based on these requirements, generate the following deliverables:

1.  **INVEST Stories:** Convert requirements into user stories using the INVEST model (As a , I want , so that ). This should be based on end user UI/UX. 

2.  **Gherkin Acceptance Criteria:** For each story, write at least one scenario in Given/When/Then format. This should be based on end user UI/UX.  

3.  **Backlog:** Organize the stories into **Epics** (e.g., CRUD, Filtering, Usability). Provide a table with:
    *   Story ID
    *   Story Description 
    *   Epic 
    *   Priority (High/Medium/Low) 
    *   Estimate (Story Points or T-shirt size) 
    *   Dependencies (if any)  
4.  **Sprint Plan:** Create a 2-sprint plan (2 weeks each) with dependencies respected (e.g., backend CRUD before UI). Present as Markdown lists. 
5.  **Risks & Assumptions:** List key assumptions made and potential risks/unknowns.
    

**Output Format:**

*   **Stories & Gherkin:** Markdown list with story text + Gherkin block.
*   **Backlog Table:** Markdown table with columns \[ID | Story | Epic | Priority | Estimate | Dependencies\].
*   **Sprint Plan:** Sprint 1 and Sprint 2 items.
*   **Risks/Assumptions:** Bullet points.
    
**Constraints:**

*   Ensure every story is **Independent, Negotiable, Valuable, Estimable, Small, Testable (INVEST)**.
*   Gherkin criteria must be specific and testable. Make sure the text is elaborate, clear and valid. 
*   Keep the backlog practical (10-20 stories is fine).
*   Provide 2 estimates, with and without AI tools help. This would give a bit the expectations of the significance of using AI tools for each task.  
*   Present everything in Markdown so it can be copied into Jira or Azure DevOps.
    
Store the results into #file:001- initial_MVP.md 