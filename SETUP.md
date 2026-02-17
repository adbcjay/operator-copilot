# Setup: Operator Copilot

## Prerequisites

- An AI coding agent that reads markdown configuration files (Claude Code, Cursor, Windsurf, Cline)
- The persona is agent-runtime agnostic but tested primarily on Claude Code

## Optional MCP Servers

No MCP servers are required. The persona degrades gracefully without any of them. But these integrations significantly expand what it can do:

### Google Drive
Enables document management, spreadsheet operations, and file organization directly from your AI session.
```bash
npx @anthropic-ai/claude-code mcp add google-drive -- npx -y @piotr-agier/google-drive-mcp
```
After adding: complete the OAuth flow to authenticate your Google account.

### n8n (workflow automation)
Enables managing n8n workflows, creating automations, and monitoring execution.
```bash
npx @anthropic-ai/claude-code mcp add n8n -- npx -y n8n-mcp
```
Requires: a running n8n instance with API access enabled. Set `N8N_API_URL` and `N8N_API_KEY` environment variables.

## Optional Skills

These skills enhance the persona's document handling capabilities:

```bash
npx skills add nichochar/xlsx      # Spreadsheet operations
npx skills add nichochar/pdf       # PDF processing
npx skills add nichochar/docx      # Word document editing
```

## After Installation

1. **Edit PERSONA.md** -- Replace any remaining `{{VARIABLE}}` placeholders with your actual information. The installer handles most of these, but review the Context section and add details about your team, industry, and working environment.

2. **Add your writing samples** -- Create `examples/writing-samples.md` with 3-5 real emails or messages you've written. The persona uses these to match your voice when drafting communications.

3. **Test it** -- Start a new session and give it a task you'd normally do. Check that the communication style feels right. The persona should push back, ask clarifying questions, and act rather than just report.

4. **Tune the behavioral rules** -- The anti-sycophancy and directness settings are calibrated for someone who wants a genuine collaborator. If the tone is too blunt for your preference, soften the Communication Style section. If it's not direct enough, add stronger rules.

## Troubleshooting

**Persona feels too generic**: Add more detail to the Context section. The more the persona knows about your company, team, and industry, the better it performs.

**Still getting sycophantic responses**: Some AI models are harder to de-sycophantize than others. If you're getting "Great question!" despite the rules, add specific examples of bad responses to the Communication Style section with "NEVER say this" annotations.

**Not acting autonomously enough**: Check the Behavioral Rules section. The "ACT, don't report" rule should drive proactive behavior. If the model is still asking permission for everything, strengthen the language.
