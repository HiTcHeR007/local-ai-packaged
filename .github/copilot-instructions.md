# Copilot Instructions for local-ai-packaged

## Überblick & Architektur
Dieses Repository bietet eine Docker-Compose-basierte Umgebung für lokale KI- und Low-Code-Entwicklung. Es integriert mehrere Services:
- **n8n**: Low-Code-Automatisierung mit AI-Agenten-Workflows (Workflows liegen unter `n8n/backup/workflows/` und als JSON in `Local_RAG_AI_Agent_n8n_Workflow.json`).
- **Supabase**: Datenbank, Vektorstore und Authentifizierung. Konfiguration und Dockerfiles unter `supabase/`.
- **Ollama**: Lokale LLMs.
- **Open WebUI**: Chat-Oberfläche für KI-Agenten.
- **Flowise**: No/Low-Code KI-Agenten-Builder (`flowise/`).
- **Neo4j**: Knowledge Graph Engine (`neo4j/`).
- **SearXNG**: Metasuchmaschine (`searxng/`).
- **Caddy**: HTTPS/TLS-Management (`Caddyfile`).
- **Langfuse**: Observability für LLM-Agenten.

## Wichtige Workflows
- **Starten aller Services**: Nutze `docker-compose.yml` im Root-Verzeichnis. Für Supabase-spezifische Services gibt es eigene Compose-Dateien unter `supabase/docker/`.
- **Build & Run Tasks**: VS Code Tasks sind vorkonfiguriert:
  - `docker-build`: Baut Supabase-Container.
  - `docker-run: release`/`debug`: Startet Supabase im Release- oder Debug-Modus.
- **n8n Workflows**: Automatisierte RAG-Agenten sind als JSON-Workflows hinterlegt und werden beim Setup in n8n importiert.
- **Testcontainers**: Beispielprojekt unter `testcontainers-cloud-java-example/` zeigt, wie Integrationstests mit Cloud-Containern laufen.

## Projekt-spezifische Konventionen
- **Umgebungsvariablen**: Supabase benötigt aktuelle Variablen (z.B. `POOLER_DB_POOL_SIZE=5`). Prüfe `.env.example` bei Updates.
- **Datenpersistenz**: Volumes für Datenbanken und Logs sind unter `supabase/docker/volumes/` und `neo4j/data/`.
- **Workflows & Custom Tools**: Flowise- und n8n-spezifische Custom Tools liegen als JSON unter `flowise/` und `n8n-tool-workflows/`.
- **Service-Kommunikation**: Services kommunizieren primär über HTTP/REST, WebSockets (Supabase Realtime), und Datenbankzugriffe.

## Integration & Erweiterung
- **Neue Workflows**: Lege neue n8n- oder Flowise-Workflows als JSON im jeweiligen Ordner ab.
- **Supabase Erweiterungen**: Eigene Funktionen/Trigger können in `supabase/` und `supabase/docker/dev/data.sql` hinterlegt werden.
- **Debugging**: Für Supabase im Debug-Modus nutze den VS Code Task `docker-run: debug` (setzt Umgebungsvariablen wie `DEBUG=*`).

## Beispiele
- **n8n RAG-Agenten**: Siehe `n8n/backup/workflows/V1_Local_RAG_AI_Agent.json`.
- **Supabase Docker-Konfiguration**: Siehe `supabase/docker/docker-compose.yml` und `supabase/Dockerfile`.
- **Flowise Custom Tools**: Siehe `flowise/create_google_doc-CustomTool.json`.

## Hinweise für AI Agents
- Bevorzugt werden Docker-Compose und VS Code Tasks für Service-Management.
- Änderungen an Workflows sollten als neue JSON-Dateien abgelegt werden.
- Prüfe `.env.example` bei Supabase-Updates auf neue Variablen.
- Für neue Komponenten: Beachte die Service-Trennung und nutze die jeweiligen Ordnerstrukturen.

---
Feedback zu unklaren oder fehlenden Abschnitten erwünscht!
