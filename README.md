[![MseeP.ai Security Assessment Badge](https://mseep.net/pr/hyson666-pdf-rag-mcp-server-badge.png)](https://mseep.ai/app/hyson666-pdf-rag-mcp-server)

# PDF RAG MCP Server
<img width="600" alt="image" src="https://github.com/user-attachments/assets/3aeb102a-6d7f-4d58-a15b-129e640b2e35" />

<img width="1614" alt="image" src="https://github.com/user-attachments/assets/2b6e12c0-48f1-49f8-8d50-db03da2d1ee8" />

A powerful document knowledge base system that leverages PDF processing, vector storage, and MCP (Model Context Protocol) to provide semantic search capabilities for PDF documents. This system allows you to upload, process, and query PDF documents through a modern web interface or via the MCP protocol for integration with AI tools like Cursor.

## Features

- **PDF Document Upload & Processing**: Upload PDFs and automatically extract, chunk, and vectorize content
- **Real-time Processing Status**: WebSocket-based real-time status updates during document processing
- **Semantic Search**: Vector-based semantic search across all processed documents
- **MCP Protocol Support**: Integrate with AI tools like Cursor using the Model Context Protocol
- **Modern Web Interface**: React/Chakra UI frontend for document management and querying
- **Fast Dependency Management**: Uses uv for efficient Python dependency management

## System Architecture

The system consists of:

- **FastAPI Backend**: Handles API requests, PDF processing, and vector storage
- **React Frontend**: Provides a user-friendly interface for managing documents
- **Vector Database**: Stores embeddings for semantic search
- **WebSocket Server**: Provides real-time updates on document processing
- **MCP Server**: Exposes knowledge base to MCP-compatible clients

## Quick Start

### Prerequisites

- [Python](https://www.python.org/downloads/) 3.8 or later
- [uv](https://github.com/astral-sh/uv) - Fast Python package installer and resolver
- Git
- Cursor (optional, for MCP integration)

### Quick Installation and Startup with uv and run.py

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/PdfRagMcpServer.git
   cd PdfRagMcpServer
   ```

2. Install uv if you don't have it already:
   ```bash
   curl -sS https://astral.sh/uv/install.sh | bash
   ```

3. Install dependencies using uv:
   ```bash
   uv init .
   uv venv
   source .venv/bin/activate
   uv pip install -r backend/requirements.txt
   ```

4. Start the application with the convenient script:
   ```bash
   uv run run.py
   ```

5. Access the web interface at [http://localhost:8000](http://localhost:8000)

6. Using with Cursor 

Go Settings -> Cursor Settings -> MCP -> Add new global MCP server, paste below into your Cursor ~/.cursor/mcp.json file. See Cursor MCP docs for more info.
```json
{
  "mcpServers": {
    "pdf-rag": {
      "url": "http://localhost:7800/mcp"
    }
  }
}
```
You could also change localhost into the host ip you deployed the service. After this confige added to the mcp json, you will see the mcp server showes at the Cursor mcp config page, switch it on to enable the server:

<img width="742" alt="image" src="https://github.com/user-attachments/assets/d9b2c97c-c535-4d2a-bcf1-2d2c6343aeb3" />


### Building the Frontend (For Developers)

If you need to rebuild the frontend, you have two options:

#### Option 1: Using the provided script (recommended)

```bash
# Make the script executable if needed
chmod +x build_frontend.py

# Run the script
./build_frontend.py
```

This script will automatically:
- Install frontend dependencies
- Build the frontend
- Copy the build output to the backend's static directory

#### Option 2: Manual build process

```bash
# Navigate to frontend directory
cd frontend

# Install dependencies
npm install

# Build the frontend
npm run build

# Create static directory if it doesn't exist
mkdir -p ../backend/static

# Copy build files
cp -r dist/* ../backend/static/
```

After building the frontend, you can start the application using the run.py script.

### Simple Production Setup

For a production environment where the static files have already been built:

1. Place your pre-built frontend in the `backend/static` directory
2. Start the server:
   ```bash
   cd backend
   uv pip install -r requirements.txt
   python -m app.main
   ```

### Development Setup (Separate Services)

If you want to run the services separately for development:

#### Backend

1. Navigate to the backend directory:
   ```bash
   cd backend
   ```

2. Install the dependencies with uv:
   ```bash
   uv pip install -r requirements.txt
   ```

3. Run the backend server:
   ```bash
   python -m uvicorn app.main:app --host 0.0.0.0 --port 8000 --reload
   ```

#### Frontend

1. Navigate to the frontend directory:
   ```bash
   cd frontend
   ```

2. Install the dependencies:
   ```bash
   npm install
   ```

3. Run the development server:
   ```bash
   npm run dev
   ```

## Usage

### Uploading Documents

1. Access the web interface at [http://localhost:8000](http://localhost:8000)
2. Click on "Upload New PDF" and select a PDF file
3. The system will process the file, showing progress in real-time
4. Once processed, the document will be available for searching

### Searching Documents

1. Use the search functionality in the web interface
2. Or integrate with Cursor using the MCP protocol

### MCP Integration with Cursor

1. Open Cursor
2. Go to Settings → AI & MCP
3. Add Custom MCP Server with URL: `http://localhost:8000/mcp/v1`
4. Save the settings
5. Now you can query your PDF knowledge base directly from Cursor

## Troubleshooting

### Connection Issues

- Verify that port 8000 is not in use by other applications
- Check that the WebSocket connection is working properly
- Ensure your browser supports WebSockets

### Processing Issues

- Check if your PDF contains extractable text (some scanned PDFs may not)
- Ensure the system has sufficient resources (memory and CPU)
- Check the backend logs for detailed error messages

## Project Structure

```
PdfRagMcpServer/
├── backend/               # FastAPI backend
│   ├── app/
│   │   ├── __init__.py
│   │   ├── main.py        # Main FastAPI application
│   │   ├── database.py    # Database models
│   │   ├── pdf_processor.py # PDF processing logic
│   │   ├── vector_store.py # Vector database interface
│   │   └── websocket.py   # WebSocket handling
│   ├── static/            # Static files for the web interface
│   └── requirements.txt   # Backend dependencies
├── frontend/              # React frontend
│   ├── public/
│   ├── src/
│   │   ├── components/    # UI components
│   │   ├── context/       # React context
│   │   ├── pages/         # Page components
│   │   └── App.jsx        # Main application component
│   ├── package.json       # Frontend dependencies
│   └── vite.config.js     # Vite configuration
├── uploads/               # PDF file storage
└── README.md              # This documentation
```

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the MIT License - see the LICENSE file for details.
