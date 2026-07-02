---
layout: default
title: "Module 3: Vector Memory"
description: "Build a working RAG pipeline with free vector databases. Supabase pgvector, ChromaDB, Convex, FAISS."
---

<div class="container" style="padding: 60px 24px 40px;">
  <div style="max-width: 760px; margin: 0 auto;">
    <div class="hero-badge" style="margin-bottom: 20px;">
      <span class="dot"></span>
      <span>Module 3 · ~2 hrs · RAG from scratch</span>
    </div>
    <h1 style="font-size: clamp(36px, 5vw, 56px); margin-bottom: 20px;">
      Vector <span class="accent">Memory</span>
    </h1>
    <p class="lede" style="font-size: 18px; color: var(--text-2); margin-bottom: 32px;">
      Embed your data, search by meaning, build a RAG pipeline. Free options only.
    </p>
  </div>
</div>

<div class="container" style="max-width: 900px; padding-bottom: 60px;">

  <div class="callout">
    <span class="icon-c">🎯</span>
    <p><strong>Goal:</strong> A working "ask my docs" app. Input: question. Output: answer grounded in your documents with citations.</p>
  </div>

  <h2>🧠 Mental model</h2>
  <ol>
    <li><strong>Chunk</strong> — split docs into ~500 token pieces with overlap</li>
    <li><strong>Embed</strong> — turn each chunk into a vector (embedding model)</li>
    <li><strong>Store</strong> — save vectors + text in a vector DB</li>
    <li><strong>Query</strong> — embed question, find top-K similar chunks</li>
    <li><strong>Answer</strong> — feed chunks + question to LLM, cite sources</li>
  </ul>

  <h2>🆚 Free vector DBs compared</h2>
  <table class="compare">
    <thead>
      <tr><th>DB</th><th>Setup</th><th>Free tier</th><th>Best for</th></tr>
    </thead>
    <tbody>
      <tr><td><strong>ChromaDB</strong></td><td><code>pip install chromadb</code></td><td>Unlimited (local)</td><td>Fastest start, prototypes</td></tr>
      <tr><td><strong>Supabase pgvector</strong></td><td>SQL + <code>create extension</code></td><td>500MB, 50k rows</td><td>Postgres fans, production</td></tr>
      <tr><td><strong>Convex vectors</strong></td><td><code>npm i convex</code></td><td>1GB, generous</td><td>Full-stack React/Next apps</td></tr>
      <tr><td><strong>FAISS</strong></td><td><code>pip install faiss-cpu</code></td><td>Unlimited (local)</td><td>Max control, offline</td></tr>
    </tbody>
  </table>

  <h2>🛠 Exercise: Build "Ask My Blog" (ChromaDB)</h2>
  <p>Time: ~90 min. Result: local semantic search over your markdown files.</p>

  <h3>Step 1: Install</h3>
  <div class="prompt">pip install chromadb sentence-transformers pyyaml</div>

  <h3>Step 2: Embed your content</h3>
  <details class="code-block">
    <summary>embed.py</summary>
    <pre><code>import chromadb
from sentence_transformers import SentenceTransformer
from pathlib import Path
import yaml

# 1. Load your markdown files
posts_dir = Path("_posts")  # or "docs/", "notes/", etc.
model = SentenceTransformer("all-MiniLM-L6-v2")
client = chromadb.PersistentClient(path="./chroma_db")
col = client.get_or_create_collection("my_docs")

# 2. Chunk + embed + store
for md_file in posts_dir.glob("*.md"):
    text = md_file.read_text(encoding="utf-8")
    # Simple chunking: split by headers, max ~500 chars
    chunks = []
    for section in text.split("\n## "):
        if len(section) > 100:
            chunks.append(section[:500])
    
    embeddings = model.encode(chunks).tolist()
    ids = [f"{md_file.stem}-{i}" for i in range(len(chunks))]
    metadatas = [{"source": md_file.name, "chunk": i} for i in range(len(chunks))]
    
    col.add(documents=chunks, embeddings=embeddings, ids=ids, metadatas=metadatas)
    print(f"Indexed {md_file.name}: {len(chunks)} chunks")

print(f"Total: {col.count()} chunks in ChromaDB")
</code></pre>
  </details>

  <h3>Step 3: Search + answer</h3>
  <details class="code-block">
    <summary>search.py</summary>
    <pre><code>import chromadb
from sentence_transformers import SentenceTransformer
import openai, os

client = chromadb.PersistentClient(path="./chroma_db")
col = client.get_collection("my_docs")
model = SentenceTransformer("all-MiniLM-L6-v2")
llm = openai.OpenAI(base_url="https://openrouter.ai/api/v1", api_key=os.getenv("OPENROUTER_API_KEY"))

def ask(question: str):
    # 1. Embed question
    q_emb = model.encode([question]).tolist()[0]
    
    # 2. Retrieve top-5
    results = col.query(query_embeddings=[q_emb], n_results=5)
    chunks = results["documents"][0]
    metas = results["metadatas"][0]
    
    # 3. Build context
    context = "\n\n".join([f"[Source: {m['source']}]\n{c}" for c, m in zip(chunks, metas)])
    
    # 4. Ask LLM
    prompt = f"""Answer using ONLY the context below. Cite sources like [Source: file.md].
    If context doesn't contain the answer, say "I don't have enough information."

    Context:
    {context}

    Question: {question}
    Answer:"""
    
    resp = llm.chat.completions.create(
        model="google/gemini-2.0-flash-exp:free",
        messages=[{"role": "user", "content": prompt}],
        temperature=0.1
    )
    return resp.choices[0].message.content

# Test it
while True:
    q = input("\n❓ Question (or 'quit'): ")
    if q == "quit": break
    print(f"\n🤖 {ask(q)}")
</code></pre>
  </details>

  <h3>Step 4: Web UI (optional)</h3>
  <p>Copy <code>search.html</code> from <a href="{{ '/starter-kits/' | relative_url }}#kit-p1">Starter Kit P1</a> — vanilla JS, calls a Python HTTP server, renders results with citations.</p>

  <h2>✅ Done criteria</h2>
  <ul>
    <li>☐ <code>python embed.py</code> runs without errors</li>
    <li>☐ <code>python search.py</code> answers questions about your content</li>
    <li>☐ Answers cite sources (file names)</li>
    <li>☐ "I don't know" when question is out of scope</li>
    <li>☐ (Bonus) Deploy as a simple web app on GitHub Pages + Cloudflare Workers</li>
  </ul>

  <h2>🔁 Try the other DBs</h2>
  <p>Same pattern, different client. Swap the embed/store/retrieve calls:</p>
  <div class="grid grid-2">
    <div class="card">
      <h3>Supabase pgvector</h3>
      <div class="prompt"># SQL schema
create extension vector;
create table docs (
  id bigserial primary key,
  content text,
  embedding vector(384),
  source text
);
create index on docs using hnsw (embedding vector_cosine_ops);

# Python
import psycopg2
conn = psycopg2.connect(os.getenv("SUPABASE_URL"))
# INSERT ... embedding = %s::vector
# SELECT content FROM docs ORDER BY embedding <-> %s::vector LIMIT 5
      </div>
    </div>
    <div class="card">
      <h3>Convex vectors</h3>
      <div class="prompt"># convex/schema.ts
import { defineSchema, defineTable } from "convex/server";
import { v } from "convex/values";

export default defineSchema({
  docs: defineTable({
    content: v.string(),
    embedding: v.array(v.float64()),
    source: v.string(),
  }).vectorIndex("by_embedding", {
    vectorField: "embedding",
    dimensions: 384,
    filterFields: ["source"],
  }),
});

# convex/search.ts
export const search = query({
  args: { embedding: v.array(v.float64()) },
  handler: async (ctx, args) => {
    return await ctx.db.query("docs")
      .withVectorIndex("by_embedding", (q) => q.nearest(args.embedding, 5))
      .collect();
  },
});
      </div>
    </div>
  </div>

  <h2>📚 Prompting patterns for RAG</h2>
  <div class="prompt"># System prompt for RAG agent
"You are a research assistant with access to a vector memory.
When asked a question:
1. Search memory for relevant chunks (top-5)
2. Synthesize answer citing sources like [Source: filename.md]
3. If confidence < 80%, say 'I don't have enough info' and suggest what to index"
</div>

  <h2>🔗 Resources</h2>
  <ul>
    <li><a href="https://www.trychroma.com/docs" target="_blank">ChromaDB docs</a></li>
    <li><a href="https://supabase.com/docs/guides/database/extensions/pgvector" target="_blank">Supabase pgvector</a></li>
    <li><a href="https://docs.convex.dev/vector-search" target="_blank">Convex vector search</a></li>
    <li><a href="https://github.com/facebookresearch/faiss" target="_blank">FAISS (Meta)</a></li>
    <li><a href="https://sbert.net/" target="_blank">SentenceTransformers models</a></li>
    <li><a href="{{ '/starter-kits/' | relative_url }}#kit-p1">Starter Kit P1: Blog + Search</a></li>
    <li><a href="{{ '/starter-kits/' | relative_url }}#kit-p5">Starter Kit P5: Ask-My-Repo</a></li>
  </ul>

  <div class="hero-actions" style="margin-top: 40px;">
    <a href="{{ '/starter-kits/' | relative_url }}" class="btn btn-primary">⚡ Try a starter kit</a>
    <a href="{{ '/syllabus/' | relative_url }}" class="btn btn-ghost">← Back to syllabus</a>
  </div>

</div>