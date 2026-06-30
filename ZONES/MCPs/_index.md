---
zone: MCPs
type: index
updated: 2026-06-03
---

# MCPs — Index

## Faol MCPs

| MCP | Nomi | Ishlatiladi | Zone |
|-----|------|-------------|------|
| **telegram** | plugin:telegram | Saidazim bilan muloqot, guruhga yuborish | Barcha |
| **computer-use** | mcp__computer-use | Desktop nazorat, screenshot | Barcha |
| **computer-control-mcp** | computer-control-mcp | PyAutoGUI + OCR, 15 tool, oyna boshqaruv | Barcha |
| **Gmail** | mcp__claude_ai_Gmail | Email | — |
| **Google Calendar** | mcp__claude_ai_Google_Calendar | Kalendar | — |
| **Google Drive** | mcp__claude_ai_Google_Drive | Drive fayllari | — |
| **antigravity (`agy`)** | CLI (Google) | Ikkinchi fikr + self-critic, [[antigravity-cli]] | Barcha |

## Telegram MCP

```
Chat IDs:
  Saidazim personal:      6299152655
  TEZCODE Team Mgmt:     -1002640882371
  Tezcode AI COUNSIL:    -1003874059304

Bot token (tg-notify.sh):  8710780612:AAGSY_LmqNufNyTTDqnTXUmzzFoQZjcF9jE
Bot token (council bot):   ~/.config/tg_autobot/config.env → TG_BOT_TOKEN
```

### Telegram MCP Qoidalari
- `chat_id` → `reply` tool
- Guruhga yuborishda `chat_id` manfiy bo'ladi (-100...)
- Fayllar: `files: ["/abs/path.mp4"]`
- Faqat matn: `text: "..."`

## computer-use MCP

### Kirish darajalari
- **Browser** (Safari, Chrome) → `read` tier: faqat screenshot
- **Terminal, VS Code** → `click` tier: click OK, lekin type va right-click YO'Q
- **Boshqa** → `full` tier

### Qoidalar
- Har safar `request_access` chaqirish
- Screenshot olmasdan click qilma
- Browser uchun claude-in-chrome MCP ni ishlatish yaxshiroq
