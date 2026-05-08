# Deploy and Host Langfuse on Railway

Langfuse is an open-source LLM observability and analytics platform. It helps teams trace, debug, evaluate, and monitor LLM applications with detailed logs, prompt versioning, user feedback collection, and cost analytics — essential infrastructure for running AI applications reliably in production.

## About Hosting Langfuse

Hosting Langfuse requires running its Next.js web application alongside a PostgreSQL database and a ClickHouse instance for high-volume trace analytics. PostgreSQL stores user accounts, projects, prompts, and configuration. ClickHouse handles the append-heavy ingestion of LLM traces and spans at scale. On Railway, all services are provisioned and networked within the same project. Redis is optionally used for rate limiting and caching. Langfuse exposes an SDK-compatible ingestion API, so your existing LLM app sends traces with minimal code changes.

## Common Use Cases

- Tracing and debugging LLM chains, agents, and RAG pipelines in production
- Evaluating prompt quality and tracking prompt version performance over time
- Monitoring LLM token usage and costs across models and users

## Dependencies for Langfuse Hosting

- **PostgreSQL** — stores users, projects, prompts, evaluations, and platform configuration
- **ClickHouse** — high-performance columnar store for LLM trace and span ingestion at scale

### Deployment Dependencies

- [Langfuse Documentation](https://langfuse.com/docs)
- [Langfuse GitHub Repository](https://github.com/langfuse/langfuse)
- [Langfuse Self-Hosting Guide](https://langfuse.com/docs/deployment/self-host)
- [Railway PostgreSQL Plugin](https://docs.railway.com/databases/postgresql)

## Why Deploy Langfuse on Railway?

Railway is a singular platform to deploy your infrastructure stack. Railway will host your infrastructure so you do not have to deal with configuration, while allowing you to vertically and horizontally scale it.

By deploying Langfuse on Railway, you are one step closer to supporting a complete full-stack application with minimal burden. Host your servers, databases, AI agents, and more on Railway.
