# Customer Support Chat with Multi-Agent RAG

This is a **Customer Support Chat Application** built using Python, LangGraph, Qdrant, and OpenAI. It uses a **Retrieval-Augmented Generation (RAG)** approach where multiple specialized AI agents work together to help users plan trips, book flights, hotels, and excursions.

## How It Works
![System Architecture](assets/multi-agent-rag-system-graph.png)
The system is designed as a graph of specialized agents:

1.  **Primary Assistant:** The main interface that routes your request.
2.  **Specialized Assistants:**
    *   **Flight Booking Assistant:** Searches and books flights.
    *   **Hotel Booking Assistant:** Finds and books hotels.
    *   **Car Rental Assistant:** Manages car rentals.
    *   **Excursion Assistant:** Recommends trip activities.
3.  **Vector Database (RAG):** The assistants use **Qdrant** to search through a database of travel options (flights, hotels, etc.) to provide accurate, real-world information.

## Tech Stack

*   **Python:** 3.12+
*   **LangGraph & LangChain:** For orchestrating the multi-agent workflow.
*   **Qdrant:** Vector database for semantic search.
*   **OpenAI:** LLM for reasoning and generating responses.
*   **SQLite:** Local database for storing transactional data.
![Database Schema](assets/travel_db_schema.png)
## Installation & Setup

### 1. Prerequisites
*   Python 3.12+
*   [uv](https://github.com/astral-sh/uv) (Recommended) or pip
*   Docker (for running Qdrant)

### 2. Environment Setup

1.  Clone the repository.
2.  Create a `.env` file (copy `.dev.env` template).
3.  Open `.env` and add your API keys:
    ```ini
    OPENAI_API_KEY=your_openai_api_key_here
    QDRANT_URL=http://localhost:6333
    ```

### 3. Install Dependencies

Using `uv` (Fastest):
```bash
uv sync
```

Or using `pip`:
```bash
uv pip install -r requirements.txt
```
or 
```bash
pip install -r requirements.txt
```

### 4. Start the Vector Database

Run Qdrant using Docker:
```bash
docker run -p 6333:6333 -p 6334:6334 qdrant/qdrant
```

### 5. Initialize Data (First Run Only)

If your database is empty, run the vectorizer to process data and load it into Qdrant:
```bash
python -m vectorizer.app.main
```

## Running the Application

To start the customer support chat:

```bash
python -m customer_support_chat.app.main
```

## Project Structure

*   `customer_support_chat/`: Main application source code.
    *   `app/assistants/`: Logic for different specialized agents.
    *   `app/tools/`: Tools agents use (search, book, etc.).
    *   `app/graph.py`: Defines the workflow graph.
*   `vectorizer/`: Utility scripts to load data into the vector database.
*   `pyproject.toml`: Project configuration and dependencies.

