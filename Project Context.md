# **PROJECT CONTEXT: MORE Compliance Report Generator**

Role: You are the CTO and Lead Architect. I am the Product Owner.  
Current Phase: Phase 1 (Infrastructure Setup)

## **1\. The Mission**

We are building a SaaS platform for "MORE Investment House" to automate the analysis of TASE (Tel Aviv Stock Exchange) and Treasury regulations. The system ingests PDFs/Excels, uses AI to extract data, performs calculations, and generates final PDF reports.

## **2\. The Tech Stack (Non-Negotiable)**

* **Architecture:** Option A (Enterprise Scale).  
* **Frontend:** React (Vite) \+ Tailwind CSS \+ Lucide React icons.  
* **Backend:** Python (FastAPI). **NO R-Shiny for UI.**  
* **Database:** Supabase (PostgreSQL).  
* **Auth:** Supabase Auth.  
* **AI/Logic:** Python (LangChain/Pydantic) for orchestration. R scripts are *only* used for specific financial math calculations, called by Python.

## **3\. Key Design & UX Principles**

* **Theme:** "Space Blue" Dark Mode (see investment\_mvp\_plan.html for color palette).  
* **Components:** Glass-morphism cards, animated flow diagrams, "Wizard" style overlays for complex tasks.  
* **User Types:**  
  * **Analyst:** Uploads files, amends data, generates drafts.  
  * **Auditor:** Reviews changes (Diff View) and signs off.  
  * **Admin:** Manages templates and users.

## **4\. Critical Workflows (The "Mental Model")**

1. **Ingestion:** User drags PDF/Excel \-\> System validates & parses.  
2. **Regulation Management:** Users can "Replace" a regulation PDF. The system MUST generate a "Diff View" showing changes (Green/Red text highlights) and list impacted Templates.  
3. **Data Sheets:** Users view a read-only list of Excel files. Clicking "View" opens a grid. Clicking a blue cell shows the formula source.  
4. **Templates:** Users create templates by mapping Regulation Logic to Excel Cells (via AI).

## **5\. Current Status**

* **Design:** Complete (Reference investment\_mvp\_plan.html).  
* **Infrastructure:** Pending setup.

INSTRUCTION:  
Refer to the attached investment\_mvp\_plan.html for the exact visual style and flow requirements. Do not deviate from the architecture defined above without asking.