# marketing_helper

Piattaforma full-stack per supportare flussi marketing con gestione clienti, brand identity e orchestrazione multi-agente.

## Stack

- Frontend: Angular + Nginx
- Backend: FastAPI
- Agent service: FastAPI + LangGraph
- Databases: PostgreSQL + MongoDB
- LLM runtime: Ollama (modello MVP `qwen3.5:2b`)

## Servizi Docker Compose

- `postgres`: persistenza relazionale
- `mongo`: storage documentale
- `ollama`: inferenza LLM locale
- `ollama-init`: pull automatico del modello al bootstrap
- `agent`: servizio multi-agente (`/agent/*`)
- `be`: API principale e gateway verso `agent` (`/api/*`)
- `fe`: applicazione Angular servita via Nginx

## Avvio rapido

```bash
docker compose up -d --build
```

Endpoint utili in locale:

- Frontend: `http://localhost:4200`
- Backend Swagger: `http://localhost:8000/swagger`
- Agent Swagger: `http://localhost:8001/swagger`
- Ollama API: `http://localhost:11434`

## Flusso agent (MVP)

Per mantenere il frontend semplice, il flusso e':

1. FE chiama `POST /api/agent/invoke` sul backend
2. Backend inoltra a `POST /agent/invoke` sul servizio agent
3. Agent esegue workflow LangGraph base (planner -> strategy -> brand -> copy)

## Note MVP

- Il workflow multi-agente e' volutamente stub iniziale.
- `qwen3.5:2b` e' scelto per footprint ridotto e bootstrap rapido.
- Le funzionalita' saranno estese incrementalmente nei prossimi step.
