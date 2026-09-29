# Academic Research Suite v3.22.2 — Personal MCP Plugin

This package wraps the bundled ARS-Codex v3.22.2 as a **read-only MCP server** for ChatGPT Developer Mode.

## What it exposes

- `ars_overview`
- `ars_load_workflow`
- `ars_load_command`
- `ars_search`
- `ars_read_file`

The server does **not** store or modify your research files. It only serves the bundled ARS workflow/agent/reference content.

## Local test

Requirements: Node.js 20+

```bash
npm install
npm start
```

Health check:

```text
http://localhost:8787/health
```

MCP endpoint:

```text
http://localhost:8787/mcp
```

Optional MCP Inspector:

```bash
npx @modelcontextprotocol/inspector@latest
```

Choose Streamable HTTP and connect to `http://localhost:8787/mcp`.

## Deploy to a public HTTPS host

The project includes a `Dockerfile` and `render.yaml`. Any host that can run a Docker/Node web service and provide HTTPS works.

On Render, deploy this repository as a Web Service. The service reads the platform-provided `PORT`; no API key or environment variable is required.

After deployment, suppose the host gives:

```text
https://academic-research-suite-mcp.example.com
```

Your ChatGPT MCP URL is:

```text
https://academic-research-suite-mcp.example.com/mcp
```

## Connect in ChatGPT

1. Settings → Security and login → turn on **Developer mode**.
2. Open **Plugins**.
3. Select **+**.
4. Enter a name such as `Academic Research Suite`.
5. Use your public HTTPS URL ending in `/mcp`.
6. Create the connection and review the discovered tools.
7. Install the resulting personal plugin if ChatGPT prompts you to do so.
8. In a new **Work** chat, invoke the plugin with `@Academic Research Suite`.

Recommended first prompt:

```text
@Academic Research Suite I have completed the statistical analysis for a clinical meta-analysis and now need to write the manuscript. Use ARS to choose the appropriate workflow, then help me draft the paper section by section. Do not rerun analyses unless I ask.
```

## Security note

This server is intentionally read-only and contains only the open-source ARS package. Do not add private manuscripts, patient data, credentials, or API keys to the server directory.
