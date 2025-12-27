# **Implementation Roadmap: MORE Compliance Engine**

**Stack:** Python (FastAPI) \+ React (Vite/Tailwind) \+ Supabase (DB/Auth)

## **Phase 1: The Foundation (Infrastructure & Data)**

**Goal:** A working backend that connects to a database and handles user login.

### **1.1 Project Initialization**

* **Action:** Create the folder structure.  
* **Cursor Prompt:**"Initialize a monorepo structure. Create a /backend folder with a basic FastAPI app (main.py, requirements.txt) and a /frontend folder with a React+Vite+Tailwind app. Include a docker-compose.yml that runs the backend on port 8000 and frontend on 3000."

### **1.2 Database Schema (Supabase)**

* **Action:** Define the data structure.  
* **Cursor Prompt:**  
  "I need a PostgreSQL schema for an Investment Compliance system. Create a SQL script for Supabase.  
  Tables needed:  
  1. users (id, email, role: \[admin, analyst, auditor\])  
  2. regulations (id, title, version, file\_url, status: \[active, archived\], effective\_date)  
  3. templates (id, name, regulation\_id, data\_source\_file)  
  4. data\_sheets (id, filename, uploaded\_by, last\_updated)  
  5. reports (id, template\_id, status, generated\_at)  
     Add Foreign Keys and indexes."

### **1.3 Authentication & Security**

* **Action:** Secure the API.  
* **Cursor Prompt:**"In /backend, install supabase-py. Create a dependency deps.py that validates the Bearer token from the Request Header against Supabase Auth. Protect the root endpoint so only logged-in users can see it."

## **Phase 2: The Core Engine (Regulations & AI)**

**Goal:** Uploading a PDF and having Python extract text from it.

### **2.1 File Storage API**

* **Action:** Allow PDF uploads.  
* **Cursor Prompt:**"Create a new API route POST /regulations/upload. It should accept a PDF file, upload it to a Supabase Storage bucket named 'raw\_regulations', and insert a record into the regulations table with 'pending' status."

### **2.2 The AI Worker (Text Extraction)**

* **Action:** The logic that reads the PDF.  
* **Cursor Prompt:**"Create a service services/ocr.py. Use PyMuPDF (fitz) or pdfplumber to extract text from a PDF bytes object. Create a function extract\_text(file\_bytes) that returns the raw text string."

### **2.3 The Diff Engine (Logic)**

* **Action:** Comparing two text versions.  
* **Cursor Prompt:**"Create a logic function that compares two strings (old regulation text vs new regulation text). It should return a list of differences (added text, removed text). Suggest using the difflib library or a lightweight NLP approach to identify changed clauses."

## **Phase 3: The Data Layer (Excel Processing)**

**Goal:** Reading the Excel Data Sheets that drive the calculations.

### **3.1 Excel Ingestion**

* **Action:** Reading .xlsx files.  
* **Cursor Prompt:**"Create an API route POST /datasheets/upload. It accepts an Excel file. Use pandas to read the file into a DataFrame. Convert the DataFrame to JSON and store it in a jsonb column in the data\_sheets table."

### **3.2 The Calculation Service**

* **Action:** Running the math.  
* **Cursor Prompt:**"Create a services/calc\_engine.py. It should take a dictionary of inputs (from the Excel JSON) and run a specific formula. For the MVP, hardcode a function calculate\_risk\_weight(assets, liabilities) that returns (assets \- liabilities) \* 0.15."

## **Phase 4: The Frontend Shell (UI Construction)**

**Goal:** A visual interface that looks like the HTML mock.

### **4.1 Global Styling**

* **Action:** Applying the "Space Blue" theme.  
* **Cursor Prompt:**"Read the investment\_mvp\_plan.html file I provided. Update tailwind.config.js and index.css to match those exact colors, gradients, and card styles. I want the app background to be that specific radial gradient."

### **4.2 Dashboard & Navigation**

* **Action:** The Sidebar and Main Layout.  
* **Cursor Prompt:**"Create a Layout component with a Sidebar on the left and content area on the right. The Sidebar should have links: Dashboard, Regulations, Templates, Data Sheets. Use lucide-react for icons. Create a dummy Dashboard page with the summary cards from the HTML mock."

### **4.3 Regulations Page (List View)**

* **Action:** Showing the data.  
* **Cursor Prompt:**"Create a Regulations page. Fetch the list of regulations from GET /regulations. Display them in a table styled exactly like the 'mock-table' class in my HTML file. Include the 'Status' badge logic."

## **Phase 5: The "Magic" Features (Interactive UI)**

**Goal:** Connecting the complex flows (Diff View, Wizards).

### **5.1 The Upload Wizard**

* **Action:** The drag-and-drop modal.  
* **Cursor Prompt:**"Create a RegulationUploadModal component. It should have a drag-and-drop zone. When a file is dropped, show a progress bar animation (fake it for 2 seconds, then hit the API). On success, show a 'View Diff' button."

### **5.2 The Diff Viewer UI**

* **Action:** The side-by-side comparison.  
* **Cursor Prompt:**"Create a DiffView page. It should accept 'oldText' and 'newText'. Display them side-by-side. Highlight lines that differ in Red (left side) and Green (right side). This connects to the backend Diff Engine we built in Phase 2."

## **Phase 6: Reporting & Export**

**Goal:** Generating the final artifact.

### **6.1 Report Generation**

* **Action:** Merging data into a final doc.  
* **Cursor Prompt:**"Create a backend endpoint POST /reports/generate/{template\_id}. It should fetch the latest Data Sheet values, run the Calculation Service, and use a library like python-docx or reportlab to generate a PDF containing the results. Return the PDF file."

### **What to start with RIGHT NOW:**

1. Open **Cursor**.  
2. Paste the **1.1 Project Initialization** prompt.  
3. Once the folders are created, come back here if you have errors, or move to **1.2**.