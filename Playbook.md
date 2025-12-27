# **The "AI-Native" Development Playbook**

### **Roles & Responsibilities**

* **You (The Product Owner):** You define *what* we are building (e.g., "I need the Regulation Upload screen"). You review the output and approve/reject.  
* **Gemini (The CTO / Architect):** I hold the "Big Picture." Come to me for database schemas, complex logic, security rules, and—most importantly—to **write the prompts for Cursor**.  
* **Cursor (The Senior Developer):** The "Hands." Cursor writes the actual files, handles the boilerplate, fixes syntax errors, and refactors code. It sees your local files, so it knows the context of your codebase.

### **The "Golden Loop" Workflow**

To build this system efficiently without knowing Python/React, follow this exact 4-step loop for every feature:

#### **Step 1: The Blueprint (Ask Gemini)**

Don't ask Cursor to "build the system." It will get confused. Instead, come to me first.

* **Your Prompt to Gemini:** *"I want to build the Regulation Upload Wizard. Please define the JSON structure for the API, the database schema for Supabase, and write a detailed prompt I can paste into Cursor to generate the backend code."*  
* **My Output:** I will give you the specific Pydantic models (Python data structures) and a highly technical prompt for Cursor.

#### **Step 2: The Backend Build (Action in Cursor)**

* **Action:** Open Cursor. Open the Composer (Cmd+I or Ctrl+I).  
* **Paste:** Paste the prompt I gave you.  
* **Result:** Cursor will generate the main.py, models.py, and database.py files.  
* **Verify:** Run the backend server. If it fails, paste the error into Cursor and say "Fix this."

#### **Step 3: The Frontend Build (Action in Cursor)**

Once the backend works, come back to me or ask Cursor directly if the task is simple.

* **Your Prompt to Cursor:** *"Reference the main.py file we just made. Now create a React component using Tailwind CSS that acts as a Wizard to upload a file to this endpoint. Make it look like the glass-morphism design in my investment\_mvp\_plan.html file."*  
* **Note:** You can drag your HTML Roadmap file into Cursor so it knows exactly what design style you want\!

#### **Step 4: The Review (You)**

* **Action:** Look at the screen. Does it match the HTML mock?  
* **Refine:** If the button is wrong, click it in Cursor (using Cmd+Click) and type: *"Make this button green and move it to the right."*

### **Critical "Cheatsheet" for this Project**

#### **1\. The "Single Source of Truth"**

Your **HTML Roadmap** (the file we just built) is your design bible.

* **Tip:** Always keep investment\_mvp\_plan.html in your project root.  
* **Cursor Prompt:** *"Read investment\_mvp\_plan.html. Extract the color palette and card styling from the CSS and apply it to this new component."* \-\> This ensures your actual app looks exactly like the slick mock we created.

#### **2\. Backend First, Frontend Second**

Never try to build the UI before the Data.

1. **Define the Data:** (e.g., "A Regulation has an ID, a Title, a Version, and a Status").  
2. **Build the API:** (Python/FastAPI).  
3. **Build the UI:** (React).

#### **3\. Handling "I don't know Python"**

If you see code you don't understand, don't worry. You don't need to read it.

* **If it crashes:** Copy the *entire* error message from the terminal. Paste it into Cursor. It will fix it 99% of the time.  
* **If Cursor gets stuck:** Copy the code and the error, paste it here (to Gemini), and ask: *"Cursor is stuck. What is the logic error here?"* I will diagnose the architectural flaw.

### **Your First Task (Action Plan)**

To start this project effectively:

1. **Install Prerequisites:**  
   * Install **Node.js** (for React).  
   * Install **Python** (for FastAPI).  
   * Install **Docker** (optional, but good for database).  
2. **Initialize with Cursor:**  
   * Open a new empty folder in Cursor.  
   * **Prompt to Cursor:** *"Initialize a new project with a Python FastAPI backend in a /backend folder and a React Vite frontend in a /frontend folder. Use Tailwind CSS for the frontend."*  
3. **Connect the Design:**  
   * Drag your investment\_mvp\_plan.html into the folder.  
   * **Prompt to Cursor:** *"I want to set up my global CSS variables in React based on the styles defined in investment\_mvp\_plan.html. Please create the index.css file matching those colors and gradients."*

This is how you turn that HTML prototype into a real SaaS without writing a single line of code yourself.