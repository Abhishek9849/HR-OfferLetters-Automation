
# **HR Offer Letters Automation – UiPath (RE-Framework with Queues)**

This project automates the **HR Offer Letter generation process** using UiPath’s **Robotic Enterprise Framework (RE-Framework)**.
It follows the **Dispatcher–Performer architecture**:

* **Dispatcher** → Reads candidate data and uploads each record to **Orchestrator Queue**.
* **Performer** → Fetches Queue Items one by one and generates Offer Letters.

---

## 🚀 **Project Overview**

The automation helps HR teams generate offer letters faster by eliminating manual document creation.
It supports:

* Reading candidate data from Excel
* Creating Queue Items with structured data
* Generating personalized offer letters (Word/PDF)
* Saving the output to a configured folder
* Logging activities using the RE-Framework
* Retry and exception handling using Queue retry mechanism

---

## 📂 **Project Structure**

```
HR-OfferLetters-Automation/
│
├── Dispatcher/
│   ├── Main.xaml
│   ├── Framework files…
│   ├── Data/
│   │   ├── CandidateData.xlsx
│   │   ├── Config.xlsx
│
├── Performer/
│   ├── Main.xaml
│   ├── Framework files…
│   ├── Data/
│   │   ├── Config.xlsx
│   │   ├── OfferLetterTemplate.docx
│
├── README.md
└── project.json
```

---

## 🧠 **How It Works**

### **1️⃣ Dispatcher – Load Candidates to Queue**

The dispatcher uses RE-Framework steps:

* Reads `CandidateData.xlsx`
* Loops through each row
* Creates a **Queue Item** in Orchestrator with candidate info (Name, Role, Salary, DOJ, etc.)
* Logs success/failure of queue upload
* Moves to next transaction until all rows are added

---

### **2️⃣ Performer – Generate Offer Letters**

The performer picks **one Queue Item at a time**:

* Extracts candidate data
* Replaces placeholders inside the offer letter template
* Generates a personalized DOCX/PDF
* Saves the file into the output folder (from Config)
* Updates queue status as **Successful** or **Failed**

---

### **3️⃣ Error Handling & Retry**

This project takes full advantage of RE-Framework:

* **System Exceptions** → Auto retry via Orchestrator queue retry settings
* **Business Exceptions** → Marked as BusinessException (no retry)
* **Detailed logs** using UiPath Robot Logs + Orchestrator

---

## ⚙️ **Key Features**

✔ Fully RE-Framework based
✔ 2-Project Architecture: Dispatcher + Performer
✔ Uses Orchestrator Queues for scalable processing
✔ Error-resilient with automatic retry
✔ Template-driven offer letter creation
✔ Suitable for enterprise HR departments

---

## 🛠 **Dependencies**

* UiPath Studio 2022+
* UiPath.System.Activities
* UiPath.UIAutomation.Activities
* UiPath.Excel.Activities
* UiPath.Word.Activities / Document Understanding (if used)
* Orchestrator Queue access

---

## 📘 **Config File (Config.xlsx)**

Typical configuration keys:

| Key            | Description                          |
| -------------- | ------------------------------------ |
| InputFile      | CandidateData.xlsx path (Dispatcher) |
| QueueName      | Orchestrator Queue name              |
| TemplatePath   | Offer letter DOCX template           |
| OutputFolder   | Folder to save generated letters     |
| MaxRetryNumber | Retry count (Performer)              |
| LogFolder      | Local log file location              |

---

## ▶️ **How to Run the Automation**

### **1️⃣ Run Dispatcher**

* Update `Config.xlsx`
* Add input data in `CandidateData.xlsx`
* Run Dispatcher Main.xaml
* Verify Queue Items created in Orchestrator

### **2️⃣ Run Performer**

* Ensure Queue Items exist
* Update performer’s `Config.xlsx`
* Run Performer Main.xaml
* Offer letters will be generated automatically

---

## 📌 **Use Cases**

* HR Offer Letter Automation
* Internship letters
* Appointment and contract letters
* Bulk recruitment automation

---

## 🤝 **Contributing**

Feel free to raise issues, fork, or submit improvements.

