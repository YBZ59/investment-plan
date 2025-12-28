# **🚀 Master Build Plan: MORE Compliance Engine**

Role: You are the Product Owner. I (Gemini) am the Architect. Cursor is the Developer.  
Goal: Build a production-ready SaaS based on the investment\_mvp\_plan.html prototype.

## **🛠️ Prerequisites (Do this once)**

Before asking Cursor to do anything, ensure your computer has the tools.

1. **Install Node.js** (for the Frontend).  
2. **Install Python** (for the Backend).  
3. **Install Docker** (Optional, but recommended for running the database locally).  
4. **Create a Folder:** Create a new empty folder on your desktop named more-compliance-engine.  
5. **Add the Blueprint:** Copy your investment\_mvp\_plan.html file into this new folder. This is critical—Cursor needs to "see" it to steal the designs.

## **Phase 1: Project Initialization**

**Goal:** Create the empty project structure and set up the foundation.

### **Step 1.1: Initialize the Monorepo**

Open your more-compliance-engine folder in **Cursor**. Open the "Composer" (Cmd+I / Ctrl+I) and paste this:  
Cursor Prompt:  
"Initialize a monorepo structure for a SaaS app.

1. Create a /backend folder. Initialize a Python FastAPI project inside it using uv or standard pip. Include main.py and requirements.txt.  
2. Create a /frontend folder. Initialize a React \+ Vite project inside it using JavaScript (not TypeScript for simplicity). Install tailwindcss, lucide-react for icons, and framer-motion for animations.  
3. Create a docker-compose.yml file in the root that spins up both services."

## **Phase 2: Database & Authentication (Supabase)**

**Goal:** Set up where data lives and how users log in.

### **Step 2.1: Define the Database**

We will use Supabase (a Postgres wrapper). You can set this up on supabase.com, or ask Cursor to generate the SQL to run locally.  
Cursor Prompt:  
"I need a SQL schema for a Compliance System. Create a file named database\_schema.sql in the root.  
It needs these tables:

* users: id (uuid), email, role (admin/analyst/auditor).  
* regulations: id, title, version\_number, file\_url, status (active/archived/pending), effective\_date.  
* templates: id, name, linked\_regulation\_id, source\_file\_url.  
* data\_sheets: id, filename, uploaded\_by\_user\_id, last\_updated.  
* reports: id, template\_id, generated\_by\_user\_id, status (draft/submitted), created\_at.  
  Add foreign keys connecting these tables."

### **Step 2.2: Connect Backend to Database**

Cursor Prompt:  
"In the /backend folder:

1. Install supabase.  
2. Create a file database.py.  
3. Write code to initialize the Supabase client using environment variables SUPABASE\_URL and SUPABASE\_KEY.  
4. Create a dependency function get\_db() that we can use in our API routes."

## **Phase 3: The Backend Logic (Python)**

**Goal:** The "Brain" that processes files and diffs.

### **Step 3.1: File Upload API**

Cursor Prompt:  
"In /backend/main.py, create a new API endpoint: POST /upload/regulation.

* It should accept a PDF file upload.  
* It should upload this file to a Supabase Storage bucket named 'docs'.  
* It should insert a new row into the regulations table with the file path and set status to 'pending'.  
* Return a success message with the new Regulation ID."

### **Step 3.2: The Diff Engine (Logic)**

Cursor Prompt:  
"Create a new file /backend/services/diff\_engine.py.  
Write a function compare\_text(old\_text, new\_text).  
Use Python's difflib to compare the strings.  
Return a structured JSON object showing:

* added: List of strings added.  
* removed: List of strings removed.  
* impact\_score: A fake logic for now (return 'High' if change count \> 5, else 'Low')."

## **Phase 4: The Frontend (Design & UI)**

**Goal:** Making it look like your HTML file. **This is where we use the HTML file heavily.**

### **Step 4.1: Styling Foundation**

Cursor Prompt:  
"Look at the file investment\_mvp\_plan.html in the root directory.

1. Update /frontend/tailwind.config.js to include the specific colors used in that HTML file (the dark mode blues/slates).  
2. Update /frontend/src/index.css to apply the global body background gradient found in the HTML file (radial-gradient(circle at 50% 0%...)).  
3. Ensure the font is 'Inter' as specified."

### **Step 4.2: The Main Layout (Sidebar)**

Cursor Prompt:  
"Create a Layout.jsx component in /frontend/src/components.

* Replicate the Sidebar from investment\_mvp\_plan.html exactly.  
* Use the Logo image from the HTML (assume logo.png is in /public).  
* Use lucide-react icons to match the icons in the HTML sidebar (Dashboard, Regulations, Templates, etc).  
* Make the sidebar fixed on the left and render children on the right content area."

### **Step 4.3: The Dashboard Page**

Cursor Prompt:  
"Create Dashboard.jsx.

* Read the 'UI Journey' tab in investment\_mvp\_plan.html.  
* Replicate the 3 top stats cards ('Total Templates', 'Reports this Month', 'Pending Audit').  
* Replicate the 'Recent Activity' and 'System Health' widgets using Tailwind classes from the HTML.  
* Make the cards clickable buttons."

## **Phase 5: The "Regulations" Page (Complex Flow)**

**Goal:** Building the Upload \-\> Diff \-\> Approve flow.

### **Step 5.1: Regulation List**

Cursor Prompt:  
"Create Regulations.jsx.

* It should fetch the list of regulations from our Python backend (GET /regulations).  
* Render a table that looks exactly like the .mock-table class in investment\_mvp\_plan.html.  
* Add a 'Upload New' button in the top right."

### **Step 5.2: The Upload Wizard**

Cursor Prompt:  
"Create a component UploadWizard.jsx.

* Style it like the 'Wizard Overlay' in the HTML file (glassmorphism modal).  
* Step 1: Drag and Drop zone.  
* Step 2: A fake progress bar that animates for 3 seconds.  
* Step 3: Success message showing '2 Modifications Detected'."

### **Step 5.3: The Diff View Screen**

Cursor Prompt:  
"Create RegulationDiff.jsx.

* It should show two panels side-by-side (Old Version vs New Version).  
* Use green background for added text and red for removed text.  
* At the bottom, add the 'Impact Analysis' section from the HTML file, listing affected templates.  
* Add 'Approve' and 'Reject' buttons."

## **Phase 6: Final Polish**

**Goal:** Connecting the wires.

### **Step 6.1: Navigation Routing**

Cursor Prompt:  
"Set up react-router-dom in /frontend/src/App.jsx.

* Route / to Dashboard.  
* Route /regulations to Regulations Page.  
* Route /regulations/diff to the Diff View.  
  Ensure the Layout component wraps all these routes."

### **Step 6.2: Final Review**

Cursor Prompt:  
"Scan the entire project. Ensure all buttons use the specific gradient styles defined in investment\_mvp\_plan.html (e.g., linear-gradient blue to purple). Fix any buttons that are just plain colors."

### **📝 How to Execute This**

1. Start with **Phase 1**. Paste the prompt. Wait for Cursor to finish.  
2. Move to **Phase 2**.  
3. If Cursor asks clarifying questions (e.g., "Do you want to use SQLAlchemy or SQLModel?"), come back to me (Gemini) and paste the question. I will give you the answer.  
4. **Crucial:** Keep investment\_mvp\_plan.html updated if you change your mind on the design.