# Samarthya Platform

Voice-first AI platform for government welfare schemes in India.

## Project Structure

```
samarthya-platform/
├── packages/                    # Shared packages
│   ├── shared-types/           # TypeScript types and interfaces
│   ├── database/               # MongoDB connection and schemas
│   ├── cache/                  # Redis cache manager
│   └── logger/                 # Winston logging infrastructure
├── services/                    # Microservices
│   ├── api-gateway/            # API Gateway (Node.js/Express)
│   ├── voice-service/          # Voice processing (Node.js/Express)
│   ├── user-service/           # User management (Node.js/Express)
│   ├── eligibility-service/    # Eligibility evaluation (Node.js/Express)
│   └── rag-service/            # RAG pipeline (Python/FastAPI)
├── .env.example                # Environment variables template
├── package.json                # Root package.json for monorepo
└── tsconfig.json               # Root TypeScript configuration
```

## Prerequisites

- Node.js >= 18.0.0
- Python >= 3.10
- MongoDB >= 6.0
- Redis >= 7.0

## Setup

### 1. Install Dependencies

```bash
# Install Node.js dependencies
npm install

# Install Python dependencies for RAG service
cd services/rag-service
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install -r requirements.txt
cd ../..
```

### 2. Configure Environment Variables

```bash
cp .env.example .env
# Edit .env with your configuration
```

### 3. Start MongoDB and Redis

```bash
# Using Docker
docker run -d -p 27017:27017 --name mongodb mongo:latest
docker run -d -p 6379:6379 --name redis redis:latest
```

### 4. Build Services

```bash
npm run build
```

### 5. Start Services

```bash
# Start API Gateway
cd services/api-gateway && npm run dev

# Start Voice Service
cd services/voice-service && npm run dev

# Start User Service
cd services/user-service && npm run dev

# Start Eligibility Service
cd services/eligibility-service && npm run dev

# Start RAG Service
cd services/rag-service
source venv/bin/activate
python main.py
```

## Development

### Running Tests

```bash
npm test
```

### Linting

```bash
npm run lint
```

### Formatting

```bash
npm run format
```

## Architecture

The platform follows a microservices architecture:

- **API Gateway**: Entry point for all client requests, handles routing and authentication
- **Voice Service**: Manages ASR and TTS via Bhashini API
- **User Service**: Handles user profiles and authentication
- **Eligibility Service**: Evaluates user eligibility for schemes
- **RAG Service**: Orchestrates document retrieval and LLM response generation

## Technology Stack

- **Backend**: Node.js, Express, TypeScript
- **RAG Service**: Python, FastAPI, LangChain, FAISS
- **Database**: MongoDB
- **Cache**: Redis
- **LLM**: Google Gemini-Flash
- **Voice API**: Bhashini API

## License

Proprietary
