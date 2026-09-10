# 🩺 ScribeShield Bharat: Edge-First Ambient Clinical Intelligence

> Offline-first ambient medical documentation platform designed for Indian Primary Health Centres (PHCs), targeting Qualcomm® Snapdragon® X Series NPUs.

---

## 📌 Problem Statement
Rural Indian PHCs handle massive outpatient volumes under severe constraints:
- **Intermittent Connectivity:** Cloud-based clinical assistants drop during rural network blackouts.
- **Data Governance (DPDP Act 2023):** Streaming patient voice and identifiable clinical conversations to remote cloud endpoints risks regulatory non-compliance.
- **Doctor Burnout:** Manually typing notes into health management systems reduces time spent on patient care.

---

## ⚡ Architecture & Solution
ScribeShield Bharat operates fully on-device at the point of care:
1. **Edge ASR & Structuring:** Unstructured Hindi/Hinglish consultation transcripts are parsed on-device, targeting the Qualcomm Hexagon™ NPU (45 TOPS) via INT8 quantized models to maintain sub-50ms latency.
2. **Clinical Standards:** Extracted entities are mapped to **SOAP format** and formatted into **ABDM-compliant FHIR R4 Bundles** using official **SNOMED CT** and **ICD-10** codes.
3. **Resilient Store-and-Forward:** Records are committed locally to an embedded transactional SQLite buffer (`PENDING_SYNC`). When network connectivity is restored, records batch-sync to the national health gateway (`SYNCED_ABDM`).
4. **Vernacular Prescription Output:** Generates clear, localized Hindi dosage slips ready for local desk thermal printers.

---

## 🛠️ Tech Stack
- **Compute:** Qualcomm® AI Hub SDK (`qai-hub`), targeting Qualcomm Hexagon™ NPU
- **Frontend / Runtime:** Streamlit (Python 3.14)
- **Local Persistence:** Transactional SQLite (Store-and-Forward queue)
- **Standards:** Ayushman Bharat Digital Mission (ABDM) FHIR R4, SNOMED CT, ICD-10

---

## 🚀 Local Setup

1. **Clone the repository:**
   ```bash
   git clone [https://github.com/rohitksingh-021/scribeshield-bharat.git](https://github.com/rohitksingh-021/scribeshield-bharat.git)
   cd scribeshield-bharat

2. **Create and activate virtual environment:**
   \`\`\`bash
   python -m venv venv
   .\venv\Scripts\Activate.ps1
   \`\`\`

3. **Install dependencies:**
   \`\`\`bash
   pip install -r requirements.txt
   \`\`\`

4. **Run the application:**
   \`\`\`bash
   streamlit run app.py
   \`\`\`