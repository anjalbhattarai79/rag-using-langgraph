# RAG with LangGraph + Google Generative AI 🚀

Concise demo of Retrieval-Augmented Generation (RAG) using Google Generative AI, LangChain components, FAISS, and LangGraph.

Why RAG? 🤔  
RAG improves model responses by augmenting generation with retrieved context from documents, keeping outputs accurate and grounded.

Pipeline Overview 🔁
1. 📄 Document Loader — PyPDFLoader reads PDF(s) into documents.
2. ✂️ Splitter — RecursiveCharacterTextSplitter breaks documents into overlapping chunks.
3. 🧠 Embeddings — GoogleGenerativeAIEmbeddings turns chunks into vector embeddings.
4. 🗄️ Vector Store — FAISS stores the embeddings for efficient similarity search.
5. 🔎 Retriever — Get the top-k similar chunks for a query.
6. 🧰 Tool — Wrap retriever in a tool (rag_tool) returning {query, context, metadata}.
7. 🤖 Model With Tools — Bind tools to the Google GenAI model (chat + tools).
8. 🕸️ Graph — LangGraph StateGraph orchestrates chat_node & ToolNode flow.
9. 💬 Chat — Use the compiled chatbot to send HumanMessage prompts and get answers grounded in retrieved context.

Quick Setup ⚙️
- Python 3.10+
- Create a .env with your Google Generative API credentials (e.g., service account / API key)
- Install requirements:
  pip install -r requirements.txt
  (or install required libs: langchain_google_genai, langchain_community, langchain_core, langgraph, faiss-cpu)

How to Run (example)
1. Load env: load_dotenv()
2. Load PDF: PyPDFLoader('AI Fellowship Nepal.pdf')
3. Split: RecursiveCharacterTextSplitter(chunk_size=1000, chunk_overlap=200)
4. Embed & store: FAISS.from_documents(chunks, GoogleGenerativeAIEmbeddings(...))
5. Create retriever: vectorstore.as_retriever(search_type="similarity", search_kwargs={"k":3})
6. Create rag_tool (retriever → returns context & metadata)
7. Bind tool to model: model.bind_tools([rag_tool])
8. Build graph: StateGraph, ToolNode, nodes & edges, compile chatbot
9. Query: chatbot.invoke({'messages':[HumanMessage(content="Your prompt...")]})

Notes 📝
- Replace model names (e.g., "gemini-2.5-flash", "gemini-embedding-001") as needed.
- Make sure to point PyPDFLoader to your PDF file path.
- Tools allow model to call the retriever during generation, enabling RAG.

License / Credits
- Example project for learning RAG with LangGraph and Google Generative AI.
