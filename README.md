# InvoiceASAP MCP server for ChatGPT and Claude

**Yes, ChatGPT, Claude and other AI agents can work with your InvoiceASAP account.** InvoiceASAP publishes no public API or official MCP server, checked 16 November 2026. Cotlet.dev connects your signed-in InvoiceASAP account to a hosted MCP server for receivables, sales reports and job photos; marking an invoice paid or changing payment settings waits for your approval.

## What you can ask

> List InvoiceASAP invoices unpaid for more than 30 days.

> Read a customer's balance, invoice aging and notes.

> Show weekly sales by item and by representative.

> Attach the before photo to estimate 1047 after I review it.

> Explain how this account accepts card, eCheck and ACH payments.

## Connect in 2 minutes

Get your API key at https://cotlet.dev/app and export it as `COTLET_API_KEY`.

### Claude Code

```bash
claude mcp add --transport http cotlet https://cotlet.dev/mcp/v1 --header "Authorization: Bearer $COTLET_API_KEY"
```

### ChatGPT

Settings → Apps → add connector URL `https://cotlet.dev/mcp/v1`, then sign in with Cotlet.dev. No API key needed.

### Cursor

Copy `.cursor/mcp.json` from this repo into your project:

```json
{
  "mcpServers": {
    "cotlet": {
      "url": "https://cotlet.dev/mcp/v1",
      "headers": {
        "Authorization": "Bearer ${COTLET_API_KEY}"
      }
    }
  }
}
```

## Run it locally (stdio)

This repo is a real MCP server. It speaks MCP over stdio, lists its InvoiceASAP tools without any key, and forwards every tool call to the hosted Cotlet.dev server. The hosted URL above stays the recommended way. Use this when your client only starts local servers.

```json
{"mcpServers":{"invoiceasap":{"command":"uvx","args":["invoiceasap-mcp"],"env":{"COTLET_API_KEY":"your-key"}}}}
```

Or with Docker:

```bash
docker build -t invoiceasap-mcp .
docker run -i --rm -e COTLET_API_KEY invoiceasap-mcp
```

Tools: `invoiceasap_guide`, `invoiceasap_status`, `invoiceasap_open`, `invoiceasap_read`, `invoiceasap_click`, `invoiceasap_type`, `invoiceasap_close`. Without `COTLET_API_KEY` a tool call answers: "Set COTLET_API_KEY. Get a key at https://cotlet.dev/app".

## Command line

Python 3.10+, nothing else to install. From PyPI:

```bash
pip install invoiceasap-mcp        # or run it once: uvx invoiceasap-mcp connect
invoiceasap-mcp connect
```

Or straight from this repo:

```bash
export COTLET_API_KEY="your-key"
python3 invoiceasap_agent.py connect   # ready config for Claude Code, Cursor, ChatGPT
python3 invoiceasap_agent.py status    # is InvoiceASAP ready in your Cotlet.dev account
python3 invoiceasap_agent.py guide     # InvoiceASAP screens and sign-in link
python3 invoiceasap_agent.py read      # open InvoiceASAP, read the page, close the browser
python3 invoiceasap_agent.py tools     # list Cotlet.dev tools
python3 invoiceasap_agent.py serve     # start the stdio MCP server (same as no argument)
```

## Questions from InvoiceASAP users

**Does InvoiceASAP have a public API or official MCP server?**

InvoiceASAP publishes no public API, official MCP server or official ChatGPT or Claude connector, checked 16 November 2026. Its documented integration is QuickBooks sync.

**How do I connect InvoiceASAP to ChatGPT?**

Sign up at https://cotlet.dev/signup?app=invoiceasap, enable InvoiceASAP and sign in at https://manage.invoiceasap.com/login.php in your Cotlet.dev Cloud Browser. Add https://cotlet.dev/mcp/v1 as the connector URL.

**Can I use Claude with InvoiceASAP?**

Yes. Add https://cotlet.dev/mcp/v1 as a custom connector in Claude, or use the Claude Code command in this repository, and sign in to Cotlet.dev.

**Is this an official InvoiceASAP MCP server?**

No. Cotlet.dev is independent and is not affiliated with InvoiceASAP, Inc. The hosted integration works in your own signed-in account.

## Find it on

- [InvoiceASAP on Cotlet.dev](https://cotlet.dev/integrations/invoiceasap-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=invoiceasap&utm_content=find)
- [PyPI package invoiceasap-mcp](https://pypi.org/project/invoiceasap-mcp/)
- [Odel](https://odel.app/modules/cotlet/invoiceasap)
- [mcpbeat](https://mcpbeat.com/mcp-servers/cotlet/invoiceasap/)
- [Step-by-step guide (PDF) on Internet Archive](https://archive.org/details/cotlet-connect-invoiceasap-to-ai-agents-guide)

## Also works with


- [All apps connected through Cotlet.dev](https://github.com/cotlet-connect)

---

More: https://cotlet.dev/integrations/invoiceasap-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=invoiceasap

Start free: https://cotlet.dev/signup?app=invoiceasap&utm_source=github&utm_medium=readme&utm_campaign=invoiceasap
