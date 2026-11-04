# ptecorefree.com uptime monitor

GitHub Actions opens https://ptecorefree.com/ every 5 minutes from GitHub's servers
(outside Contabo). On a change it sends a Telegram message through the site's existing bot:

- 🔴 DOWN (with the HTTP code; says "Cloudflare 523" when the VPS itself is unreachable)
- 🔴 still DOWN, repeated every ~30 minutes
- 🟢 back UP, with the outage length

State lives in `state.txt`, committed only when the status changes, an alert is sent, or once a week (GitHub turns off scheduled workflows after 60 days without commits). The repository should be PUBLIC: Actions minutes are free for public repos; a private repo would need ~8,000 minutes a month at this schedule (free tier: 2,000).
Three tries 20 s apart before DOWN is declared, so one slow response is not an alarm.

## Required repository secrets (Settings → Secrets and variables → Actions)

| Secret | Value |
|---|---|
| `TELEGRAM_BOT_TOKEN` | the site's Telegram bot token (vault: TELEGRAM_BOT_TOKEN) |
| `TELEGRAM_CHAT_ID`   | the admin chat id (vault: TELEGRAM_ADMIN_CHAT_ID) |

First run sends "✅ Uptime monitor active". Trigger it from Actions → "ptecorefree.com uptime" → Run workflow.
