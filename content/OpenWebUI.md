Working with RAG: 
Pipeline:
- Chunk your documents into passages: 100 - 500 tokens each 
- Compute embeddings for each chunk using a vector model (OpenAI’s text-embedding-ada-002)
- Store them into a vector database: Pinecone, Weaviate, FAISS

Query time: 
- Embed the user's query
- Vector-search your index for top-k nearest chunks
- Assemble a prompt: 
	- [SYSTEM] You're a helpful assistant
	- [CONTEXT] top - 3 chunks
	- [USER] user's question
	- Generate Answer

Using a docker container for postgres:
# pull the image (only once)
docker pull postgres:17

# run it in detached mode, exposing port 5432,
# and mounting a volume for persistence
docker run -d \
  --name postgres-test \
  -e POSTGRES_USER=testuser \
  -e POSTGRES_PASSWORD=hollowknight \
  -e POSTGRES_DB=mydb \
  -p 5432:5432 \
  -v pgdata:/var/lib/postgresql/data \
  postgres:17


# Steps
- Data Ingestion
- Text Chucking
- Embedding with OpenAI
- Storing in Postgres (via pgvector)
- Query Time retrieval
- Prompt construction and LLM call 
> Supporting multiple formats 

## Data Ingestion
### pull the image (only once)
``` bash
docker pull postgres:17
```

 run it in detached mode, exposing port 5432,  and mounting a volume for persistence
 ``` bash
docker run -d \
  --name postgres-test \
  -e POSTGRES_USER=testuser \
  -e POSTGRES_PASSWORD=hollowknight \
  -e POSTGRES_DB=mydb \
  -p 5432:5432 \
  -v pgdata:/var/lib/postgresql/data \
  postgres:17
```
### Accessing the database
``` bash
docker exec -it postgres-test psql -U testuser -d mydb
```

### Creating Dummy Data
``` SQL
-- 1) Create a new database
CREATE DATABASE rag_stock_demo;

-- 2) Connect into it
\c rag_stock_demo

-- 3) (Optional but recommended) Enable pgvector for embeddings
CREATE EXTENSION IF NOT EXISTS vector;

-- 4) Create a table of company profiles (text you’ll later embed)
CREATE TABLE company_info (
  id          SERIAL PRIMARY KEY,
  ticker      TEXT      NOT NULL,
  description TEXT      NOT NULL,
  embedding   VECTOR(1536)   -- space for text-embedding-ada-002
);

-- 5) Create a table of historical prices
CREATE TABLE stock_prices (
  id            SERIAL PRIMARY KEY,
  ticker        TEXT    NOT NULL,
  trade_date    DATE    NOT NULL,
  closing_price NUMERIC NOT NULL
);

-- 6) Populate company_info with dummy descriptions
INSERT INTO company_info (ticker, description) VALUES
  ('AAPL', 'Apple Inc. designs, manufactures, and markets smartphones, personal computers, tablets, wearables, and accessories. It also offers software services including iOS and MacOS.'),
  ('MSFT', 'Microsoft Corporation develops, licenses, and supports software, services, devices, and solutions worldwide, including Windows, Azure cloud, and Office productivity suite.'),
  ('GOOG', 'Alphabet Inc. provides online advertising services, operating search engine Google, YouTube, Android OS, and cloud computing solutions.');

-- 7) Populate stock_prices with dummy closes
INSERT INTO stock_prices (ticker, trade_date, closing_price) VALUES
  ('AAPL', '2025-07-25', 192.45),
  ('AAPL', '2025-07-24', 189.60),
  ('AAPL', '2025-07-23', 191.10),
  ('MSFT', '2025-07-25', 350.12),
  ('MSFT', '2025-07-24', 347.89),
  ('GOOG', '2025-07-25', 2730.50),
  ('GOOG', '2025-07-24', 2725.30);

-- 8) Quick sanity checks
\d company_info
\d stock_prices
SELECT * FROM company_info LIMIT 3;
SELECT * FROM stock_prices ORDER BY trade_date DESC LIMIT 5;
```
