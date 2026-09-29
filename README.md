# 🤖 AI Customer Support Agent

An AI-powered customer support system built with **Streamlit**, **LangChain**, **OpenAI**, and **MySQL**.  
It acts as an **Agent**: the LLM interprets customer queries, decides which tool to call, executes the tool, and returns a simple answer.

---

## 🚀 Project Overview
- **Frontend:** Streamlit chat interface
- **Backend:** LangChain Agent + OpenAI LLM
- **Database:** MySQL (`ecommerce` DB with `orders` table)
- **Tools:**  
  - `get_order_status(order_id)` → fetches order details  
  - `cancel_order(order_id)` → cancels an order if possible  

---

## ⚙️ Database Connection
- Configured directly in **db_service.py**:
  ```python
  DB_CONFIG = {
      "host": "localhost",
      "user": "root",
      "password": "root",
      "database": "ecommerce"
  }
Connection created with:

python
mysql.connect(**DB_CONFIG)
Queries run via cursor.execute() and results returned to the agent.

📂 Project Structure
app.py

Streamlit UI with chat input/output.

Displays conversation history.

Calls customer_support(question) for AI responses.

customer_agent.py

Loads .env for OPENAI_API_KEY.

Defines LangChain tools (get_order_status, cancel_order).

Registers tools in TOOLS dict.

Binds tools to OpenAI LLM (llm_with_tools).

Handles tool execution and final response formatting.

db_service.py

Manages MySQL connection.

get_order_status(order_id) → returns dict with order details.

cancel_order(order_id) → updates order status to CANCELLED with validation.

requirements.txt

Dependencies: openai, langchain, langchain-openai, streamlit, python-dotenv, mysql-connector-python.

.env

Stores sensitive keys:
OPENAI_API_KEY=sk-xxxx

🛠️ How the Agent Works
User asks a question in Streamlit UI.
Example: “Where is my order ORD1001?”
LLM (ChatOpenAI) interprets the query.
If tool call is needed:
For status → get_order_status
For cancellation → cancel_order
Tool executes DB query via db_service.py.
Result is passed back to LLM.
LLM formats a clear customer-friendly answer.
Streamlit displays the response.

▶️ Run Instructions
bash
# Install dependencies
pip install -r requirements.txt

# Start Streamlit app
streamlit run app.py

