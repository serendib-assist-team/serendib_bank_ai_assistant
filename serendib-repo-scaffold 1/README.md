# Serendib Bank AI Assistant

Group A · Case 1 (Serendib Bank, banking and finance)
HNDDSFTM0605 Generative AI for Information Access · NIBM · Group Project (20% of the module)
Lecturer: Anjana Jayasinghe

This page lists what the group **must** do, taken from the Group Project Brief and the Case Studies. Read it fully before you start. Design decisions, tools and plans will be recorded elsewhere (the project charter and the docs folder), not here.

---

## 1. The task

The group acts as the AI team of a company. We must design, build, test and present a working AI assistant, from raw documents to a running application. It must use retrieval-augmented generation (RAG) and agentic AI, and meet the standards a real software company would expect.

The assistant must:

- answer questions from a real document collection, with citations, and refuse when the documents do not support an answer;
- use a knowledge graph for exact facts;
- act as an agent: decide which tool to use, use at least three tools, and ask the user to confirm before it changes anything;
- run as a complete application on our own computers (localhost), with a web interface;
- be tested with numbers, to show how well it works.

## 2. Our case: Serendib Bank (fictional)

A licensed commercial bank with about 90 branches and a call centre in Colombo, offering savings accounts, fixed deposits, credit cards and personal loans.

**Problem:** about 4,000 calls a day. Most callers ask what a product costs, what its conditions are, how two products compare, and how to make a complaint. Answers are spread across long PDFs (tariff schedules, product terms, customer charters, Central Bank regulations). Agents search by hand while the customer waits. Wrong fees or out-of-date rates cause complaints and refunds, the bank cannot show a regulator where an answer came from, and some complaints are never recorded.

**Who is affected:** call-centre agents, customers, and the compliance team.

**What the bank wants:**

- exact answers about products and fees in seconds, not minutes;
- every answer traceable to an approved document and its date;
- no complaint lost: each one recorded and followed up;
- fewer complaints caused by wrong information.

**What the bank insists on:**

- numbers must be exact (a wrong fee or rate is worse than no answer);
- the assistant must never give investment or personal financial advice;
- no real customer data while the system is being built;
- the bank's own documents are not ready, so the prototype uses public documents from licensed banks and the Central Bank of Sri Lanka.

**Questions the group must answer (in the charter):**

- Which user do we help first: the agent, the customer or the compliance team? Why?
- Which ten questions do callers ask most? Which need an exact number?
- When the answer is not written in a document but must be worked out, how does the system get it right?
- What may the assistant do on its own, and what must a person confirm first?
- How do we show that every answer is correct and traceable?

We may narrow the problem (for example, fewer banks or products) and must explain what we narrowed and why in the charter.

## 3. Requirements (R1 to R9)

| # | Requirement | What "done" looks like |
|---|---|---|
| R1 | Data pipeline | At least 150 pages (or 100 documents) from at least 2 public sources, in at least 2 formats (for example PDF and web pages). A script that ingests, cleans and chunks them and can be rerun. Every chunk keeps its source, page or section, and date. A data source register lists each source, its link, its licence or permission, and the date collected. |
| R2 | Hybrid retrieval | BM25 and dense search fused with reciprocal rank fusion, then a cross-encoder reranker. At least one metadata filter (for example by date or category). Results stored in a vector database. |
| R3 | Knowledge graph | An ontology with at least 8 classes and 6 relations, and at least 150 triples. At least part of the graph is built from the documents by code. The agent queries it with SPARQL when it runs. |
| R4 | Grounded answers | Answers use only retrieved passages and graph facts. Every claim is cited to its source and page or section. The assistant says "I could not find this in the documents" when evidence is missing. Follow-up questions are rewritten using the chat history. |
| R5 | Agentic workflow | A LangGraph agent that chooses between at least three tools: document search, a knowledge graph query, and at least one action tool that changes something (for example a record in a SQLite database). Action tools need user confirmation first. The agent has a step limit, checks tool inputs, and saves a trace of every run. |
| R6 | Complete application | A FastAPI backend and a Streamlit or Gradio web interface that shows the answer, the sources and the tool calls. Runs on localhost by following the README. Settings and keys come from a `.env` file, never from the code. |
| R7 | Evaluation | At least 30 test cases: 10 normal questions, 5 multi-hop, 5 that the documents cannot answer, 5 tool tasks and 5 follow-ups. Report Recall@5 and MRR, answer correctness and faithfulness (LLM judge, with at least 10 answers checked by hand), agent task success, and response time (median and 95th percentile). Compare a simple baseline with the final system. One script reproduces all the numbers. |
| R8 | Good engineering | A GitHub repository shared with the lecturer. Each member makes at least 3 meaningful commits in their own name. A README that explains how to set up and run the system, and a `.env.example`. No keys in the repository. A `v1.0` tag at hand-in. |
| R9 | Zero cost | Only open-source software and free services (no payment card). The README lists the licence of each main library and data source. |

**Zero cost, open source only.** Paid APIs are not allowed. The system must keep working within Groq's free limits, with a short wait and retry on rate limits so the app does not crash.

## 4. Milestones

Deadlines are at 11:59 pm on the date shown.

| Date | What | Marked? |
|---|---|---|
| Fri 27 Nov 2026 · Session 3 | Brief and case studies released. Read the case, choose the group leader, start the AI-use log | No |
| Before Fri 27 Nov | Contact group members, make a group chat | No |
| Tue 1 Dec 2026 | Leader emails anjanaj@vl.nibm.lk with the leader's name, the group letter and the GitHub repository link | No |
| Tue 8 Dec 2026 | Project charter on the LMS (about two pages, template appears Sun 6 Dec): users and problem; scope; data source register; five competency questions; tools; architecture sketch; plan for the two checkpoints | No (feedback) |
| Fri 11 Dec 2026 · Session 5 | Charter meeting with the lecturer, about 7 minutes per group | No (feedback) |
| Fri 18 Dec 2026 · Session 6 | Checkpoint 1, walking skeleton: 5-minute demo on localhost. Documents in, hybrid search, an answer with a citation | No (feedback) |
| Fri 8 Jan 2027 · Session 8 | Checkpoint 2: 5-minute demo of the agent using its tools and the knowledge graph, with first evaluation numbers | No (feedback) |
| Tue 2 Feb 2027 | Final hand-in on the LMS (group and individual) | **Yes** |
| Fri 5 Feb 2027 · Session 10 | Final presentation, 35 minutes per group | **Yes** |

No class on Fri 25 Dec, Fri 15 Jan or Fri 22 Jan. The lecturer will announce any date changes on the LMS.

## 5. What to hand in (Tue 2 Feb 2027)

**As a group**

- Repository: the GitHub link with the `v1.0` tag. It must run from a clean start by following the README.
- Technical design document (about 2,500 to 3,000 words) with seven sections: 1 Problem, users and success measures (300 words); 2 Data (400); 3 Architecture (600); 4 Knowledge graph (300); 5 Agent (400); 6 Evaluation (500); 7 Running and next steps (300).
- Evaluation results: the test set (CSV) and the results table, produced by the evaluation script.
- Backup demo video: 3 minutes at most.

**Each student, individually** (Individual Submission Template, appears on the LMS on Sun 31 Jan)

- Reflection (about 500 words): what you built, one problem you solved, and what you would do differently.
- AI-use log: a table with columns date, AI tool, what you asked, what you used from the answer, what you changed, and how you checked it was right. **Start now and add to it every week.**

## 6. Final presentation (Fri 5 Feb 2027)

35 minutes per group:

1. Presentation and live demo (15 minutes, group). The demo should show a cited answer, a knowledge graph fact, an agent task with confirmation, and one refusal when the documents do not answer.
2. Peer panel questions (5 minutes). The panel for our presentation is Group B. Our group sits on the panel for Group D and must submit the Peer Panel Evaluation Form on the LMS by 11:59 pm on Fri 5 Feb.
3. Individual Q&A (15 minutes, individual marks). The lecturer chooses who answers. No notes and no AI tools. Each student gets two or three questions: about their own component, about another part of the system or the end-to-end flow, and a "what if" question. We may be asked to open our code or run a small change live.

**Everyone must understand the whole system, not only their own part.**

## 7. Marking

100 marks, scaled to 20% of the module. 40 marks are for the group and 60 for each student individually.

| Group mark (40) | Marks |
|---|---|
| End-to-end system and live demo | 15 |
| Engineering quality | 10 |
| Evaluation | 10 |
| Design document and presentation | 5 |

| Individual mark (60) | Marks |
|---|---|
| Q&A: your own component | 20 |
| Q&A: the whole system | 15 |
| Q&A: reasoning and trade-offs | 10 |
| Q&A: communication | 5 |
| Contribution and AI-use log | 10 |

**Understanding rule:** if a student scores below 20 out of 50 in the four Q&A criteria, the group mark for that student is capped at 20 out of 40. A student who did not contribute may have their group mark reduced. A student who misses the final presentation without a valid reason receives 0 for the Q&A.

## 8. Rules for every member

- **AI tools:** allowed to help us learn, code and write, but every use must be recorded in the AI-use log, and we must understand everything we submit. If we cannot explain it, it does not count. Follow NIBM's academic integrity rules.
- **Data and privacy:** use only public documents or documents we have written permission to use. No personal data in documents, test cases, screenshots or logs. Anything invented must be labelled fictional or synthetic. Check each source's licence or terms, and download politely.
- **Keys and secrets:** keep keys in a `.env` file that is never committed. A key found in the repository loses marks.
- **Commits:** everyone writes code and commits it in their own name, at least 3 meaningful commits each.
- **Zero cost:** no paid APIs and no payment cards.
- **Late submission:** late submissions lose marks.

## 9. Free tools named in the Brief

Groq free tier or Ollama (language model), sentence-transformers (embeddings and reranking), rank_bm25, FAISS, Chroma or Qdrant (search), rdflib (knowledge graph, Turtle and SPARQL), LangGraph (agent), FastAPI with Streamlit or Gradio (application), RAGAS or our own metrics code (evaluation), Git and GitHub.
