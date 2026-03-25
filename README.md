# bragfast-skills

Claude Code skills for [brag.fast](https://brag.fast) — generate branded release announcement images and videos.

## Prerequisites

Add the MCP server first:

```bash
claude mcp add bragfast -- npx -y @bragfast/mcp-server
npx @bragfast/mcp-server login <your-api-key>
```

Get an API key at [brag.fast/dashboard/account](https://brag.fast/dashboard/account).

## Install

```bash
# Install all skills
npx skills add rob-vb/bragfast-skills

# Install specific skill
npx skills add rob-vb/bragfast-skills --skill bragfast
```

## Skills

| Skill | Description |
|-------|-------------|
| `/bragfast` | Generate release images or videos. Reads your conversation context to auto-compose slides. |

## License

MIT
