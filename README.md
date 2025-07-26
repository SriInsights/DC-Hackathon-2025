# DC-Hackathon-2025
🏛️ Regulatory Comment Linkage - Mirrulations Hackathon Project
This project aims to link public comments to the specific regulatory documents they respond to within a single docket, using a mix of metadata, time-window heuristics, and semantic similarity techniques.

Contributors of this projects are

Henry Ham
Sridhar Gundumalla
Kumar H
Queyen Le
Srishti Kama
Rebakh 

https://files.slack.com/files-pri/T02GC3VEL-F097GGZBS5R/96cb94cb-e67e-484b-bdc5-8479b935d741.png

📌 Objective
To create a transparent and efficient system that:

Connects public comments to their corresponding regulatory documents (e.g. RFI, Proposed Rules, Final Rule)

Supports text-based analytics such as topic modeling, clustering, and sentiment analysis

Enables searchable exploration of comments and their relevance to policy changes

📂 Inputs
Single Docket dataset

All regulatory documents (with metadata)

All public comments (submitted directly or via attachments)

🔄 Workflow
1. 🗂️ Document Inventory
Created an inventory of all documents in the docket with:

File metadata

Document types (e.g., RFI, NPRM, Final Rule)

posted_date, document_id, etc.

2. 🧹 Comment Preprocessing
Prepared a clean dataset of comments:

Unified timestamps

Normalized column names

Mapped each comment to its docket

3. ⏳ Time-Window Matching
Linked each comment to its most likely source document:

Sorted documents by posted_date, assigned sequential doc_order

Used pandas.cut() to bin comments into doc-based time intervals

Inner merge to assign document to comment

4. 📄 Text Extraction
Extracted plain text from regulatory documents:

Handled HTML, PDF, TXT via BeautifulSoup, pdfminer, and manual fallback

Added doc_text field to each document

5. ✂️ Context Isolation
Isolated document sections most likely to contain public engagement:

Extracted text between first and last “commenter” references or keyword triggers

Used basic NLP slicing techniques

6. 🧠 Comment-Document Matching
Compared each comment with extracted document sections:

Used semantic similarity (e.g., BERT embeddings)

Measured match confidence to prioritize relevance

🚧 Gaps & To‑Dos
🔍 Validate window matching logic for edge cases (e.g., comments right after a new rule is posted)

🧽 De-duplicate/QC text extraction, especially for PDFs with encoding issues

📊 Analytics: topic modeling, keyword-in-context, clustering, sentiment tagging

🌐 UI/UX: Build a searchable dashboard for policymakers, journalists, and researchers

🧰 Tech Stack
Python: pandas, BeautifulSoup, pdfminer.six, transformers, scikit-learn

NLP: BERT embeddings, cosine similarity

Visualization: Streamlit / Dash (planned)

Data Source: Mirrulations Public S3

🤝 Acknowledgements
This project was developed as part of the 2025 Mirrulations Hackathon to improve transparency in U.S. federal rulemaking and civic tech engagement.
