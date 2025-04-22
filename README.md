# Self‑Directed Learning Assistant

A Python‑based Jupyter‑notebook application that walks a learner from initial goal‑setting to a personalized, research‑driven study plan and exportable report.

# Setup Instructions
1.Clone the repo

git clone https://github.com/<your‑user>/self‑directed‑learning‑assistant.git
cd self‑directed‑learning‑assistant

2.Create / activate a virtual environment (optional but recommended)

python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate

3.Install dependencies

pip install -r requirements.txt

Key libraries: faker, matplotlib, networkx, markdown, graphviz (system‑level), ipython.

4.(Colab) One‑click launch
If you prefer Google Colab, open notebook.ipynb with the Colab badge in the repo; the first code cell installs OS‑level Graphviz with apt-get automatically.

# System Architecture

The notebook is organised as five sequential stages:

*Interactive Questioning – prompts the learner for topic, objectives, knowledge level, preferred formats, depth and time budget. Answers are stored in a single user‑profile dictionary shared across the runtime.

*Research Simulation – ResearchSimulator fabricates realistic web articles, YouTube‑style videos, and academic papers. In production these stubs can be replaced by real search, YouTube Data, and Google Scholar APIs without touching later code.

*Content Organisation – LearningContentOrganizer selects key concepts, stitches explanatory text, optional step‑by‑step examples and (where requested) auto‑generated visualisations.

*Report Generation – LearningReportGenerator converts the organised content into one continuous Markdown document, embeds any PNG visuals, and immediately renders it inside the notebook.

*Follow‑Up Loop – a simple CLI loop lets the learner ask questions, request clarification, or suggest improvements; each action mutates the in‑memory learning path so new Q&A or examples appear in the final export.

# Research Methodology

Web content, video transcripts, and academic papers are produced on‑the‑fly with Faker. Titles, URLs, snippets, authors, journals, DOIs, even timestamped transcripts mirror the structure of genuine sources so the downstream pipeline (summaries, citations, excerpts) can be tested end‑to‑end. When moved to production, the simulator functions can be swapped for real API calls; no other part of the notebook needs to change.

# Personalisation Approach

Every choice the learner makes in the opening interview shapes the learning path:

Knowledge level limits how many key concepts are included (five for beginners up to fifteen for experts).

Interest keywords are woven into fabricated snippets and also spawn additional " in " concepts.

Preferred formats trigger conditional content: examples for "step‑by‑step examples" and PNG figures for "diagrams/visualisations".

Depth and time budget govern the breadth of coverage and are echoed back in the report header for planning.

# Report Generation and Modification

The generator writes a Markdown document comprising header, table of contents, individual concept modules, and a summary. Visualisations created with Matplotlib/NetworkX are saved alongside the report and referenced with standard Markdown image syntax so GitHub will render them immediately.

During the follow‑up loop the learner can:

ask a question → stored with its answer under the final module;

request clarification → an extra explanatory paragraph is appended to the chosen section;

suggest an improvement → e.g. "more examples" adds an additional enumerated example block.

Once satisfied, the learner can export both .md and .html versions directly from the notebook; the Colab runtime uses files.download for instant retrieval.

# Limitations and Future Improvements

Synthetic content – The current build is a sandbox. Swapping in live search and citation validation is the first production step.

Answer quality – Follow‑up answers are random prose; a retrieval‑augmented language model will replace this placeholder.

Session persistence – At present everything lives in memory; a lightweight database or cloud storage layer will allow users to resume later.

User interface – Notebook prompts are functional but spartan. A Streamlit or React front‑end would provide a smoother experience and richer widgets.

Learning analytics – No quizzes or spaced‑repetition metrics yet; these will be added to help users measure retention.
