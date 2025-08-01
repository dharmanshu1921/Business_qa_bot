# Business QA Bot (Retrieval-Augmented Generation)

A robust **retrieval-augmented QA assistant** purpose-built for business policy and HR document questions. This bot uses the LangChain framework, OpenAI embeddings and models, and Pinecone vector database to provide **professional, context-informed answers** based on your own documents.

## 🚀 Features

- **Contextual Answers:** Uses company documents or handbooks to answer business, policy, and HR-related queries.
- **Retrieval-Augmented:** Finds and cites relevant document chunks to justify answers.
- **Business-Focused:** Default prompt makes it ideal for policy, benefits, HR, operations, and compliance Q&A.
- **Conversational Interface:** Simple command-line or notebook experience with suggested follow-up questions.
- **Sample Data Generation:** Includes a utility to create a sample business policy PDF for demonstration or testing.

## 🛠️ Setup

### 1. Install Dependencies

```bash
pip install -U langchain-openai langchain-pinecone tiktoken fpdf
pip install "unstructured[md]" pdf2image pypdf
```

### 2. Environment Variables

Store your Pinecone and OpenAI API keys as environment variables or in your notebook (e.g., Colab):

```python
import os
os.environ['PINECONE_API_KEY'] = 'your-pinecone-key'
os.environ['OPENAI_API_KEY'] = 'your-openai-key'
```

### 3. Usage

**Notebook or Script Example:**

```python
# 1. Create a sample document (or use your business PDF)
policy_pdf = create_sample_policy_pdf()  # or use your own PDF

# 2. Process the document
document_chunks = load_and_split_documents(policy_pdf)

# 3. Create Pinecone vector store
vector_db = setup_vector_store('business-qa-rag', document_chunks)

# 4. Create the QA system
qa_bot = create_qa_system(vector_db)

# 5. Ask questions!
query = "What health insurance do we offer?"
result = qa_bot.invoke({"query": query})

# 6. Get answer and sources
print(result['result'])
print(format_source_documents(result['source_documents']))
```

or run the full interactive loop called in `__main__`.

## 🧩 Core Components

| Component           | Description                                                    |
|---------------------|----------------------------------------------------------------|
| Document Loader     | Splits PDFs using `langchain_community.document_loaders`       |
| Vector Store        | Uses Pinecone with OpenAI Embeddings (text-embedding-3-large)  |
| LLM                 | OpenAI GPT-4 Turbo (`gpt-4-turbo`) for answering               |
| QA Chain            | RetrievalQA from LangChain with custom business prompt         |
| Demo Data           | Utility to generate sample company policy PDF                  |
| Interactive Mode    | CLI/chat-like loop with auto-suggestions for follow-ups        |

## 📄 Sample Questions

- What's the standard refund window?
- How much does express shipping cost?
- What health insurance do we offer?
- How many vacation days do employees get?
- What’s our uptime guarantee?
- Where is our office located?

## ⚡ Demo Walkthrough

```
🤖 Welcome to the GlobalTech Business Assistant!

Your business question (type 'exit' to quit): What health insurance do we offer?
🤖 ANSWER: GlobalTech Solutions offers a Cigna PPO plan for health insurance.

🔍 SOURCES:
1. 📄 Page 1: GlobalTech Solutions - Company Policies 3. Employee Benefits 3.1 Health insurance: Cigna PPO plan...

💡 Try asking about our policies: refunds, shipping, or employee benefits
```

## 🔒 Security & Notes

- Requires valid Pinecone and OpenAI API keys.
- For **production use**, connect to your real business policy/HR PDFs or docs instead of the demo file.


## 🤝 Acknowledgments

- [LangChain](https://github.com/hwchase17/langchain)
- [Pinecone Vector Store](https://www.pinecone.io/)
- [OpenAI](https://openai.com/)
- [PDF handling by FPDF, PyPDF, Unstructured]

**Contributions welcome!** Submit PRs for new loaders, UI integrations, or general improvements.
