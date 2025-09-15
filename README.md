<img width="813" height="745" alt="image" src="https://github.com/user-attachments/assets/7165128f-efda-456e-a2d6-aa5ad9e53113" />


Meeting Transcript Flow – n8n Automation
📌 Overview

This workflow automates the process of retrieving a meeting transcript from Google Drive, processing it with LangChain + OpenAI embeddings, storing it in Pinecone, and enabling Telegram-based Q&A using GPT.

The goal is to let users query the meeting transcript in natural language via Telegram and get precise, transcript-based answers — avoiding unrelated or speculative responses.

⚙️ Workflow Components
Step	Node	Purpose
1	Google Drive Trigger	Monitors a specific transcript file in Google Drive for updates.
2	Download File	Fetches the transcript (PDF) whenever it changes.
3	Recursive Character Text Splitter	Breaks the transcript into manageable chunks (100 tokens, 5-token overlap).
4	Default Data Loader	Converts binary data (PDF) into text format for processing.
5	Embeddings OpenAI	Generates embeddings (vector representations) of the transcript.
6	Pinecone Vector Store	Stores embeddings in Pinecone for semantic search and retrieval.
7	Telegram Trigger	Listens for incoming user messages in Telegram.
8	AI Agent (LangChain)	Handles queries, retrieves relevant chunks from Pinecone, and formulates responses using GPT.
9	OpenAI Chat Model	Processes natural language queries (using GPT-3.5-turbo).
10	Simple Memory	Maintains short-term conversation context per Telegram user session.
11	Send a Text Message	Replies to the user with AI-generated answers on Telegram.
🔗 Tech Stack

n8n – Workflow automation

Google Drive API – File watch & download

LangChain – Document loading, splitting, and embedding pipeline

OpenAI GPT-3.5 – Conversational AI for answering queries

Pinecone – Vector database for semantic search

Telegram Bot API – User interaction interface


🚀 Setup Instructions
Import Workflow

Open n8n → Go to Workflows → Import from File → Select Meeting Transcript flow.json.

Configure Credentials

Google Drive OAuth – Connect your Google Drive account.

OpenAI API Key – Add your key in the OpenAI credential section.

Pinecone API Key – Provide index name & key.

Telegram Bot Token – Create a bot via @BotFather and configure in n8n.

Activate Workflow

Turn the workflow ON so it runs automatically on file updates.

Test the Bot

Send a query like “What was discussed about project deadlines?” to your Telegram bot and receive transcript-based answers.

🎯 Key Features
✅ Fully Automated – No manual transcript parsing.

✅ Context-Aware Responses – Answers are grounded in transcript data.

✅ Real-Time Updates – New transcript versions are automatically indexed.

✅ Scalable – Works with multiple transcripts if required (with minor tweaks).

📌 Notes
Ensure your Pinecone index has 512 dimensions (to match embedding size).

OpenAI usage will incur token costs based on query volume.

If transcript size is large, consider adjusting chunk size and overlap for better results.

