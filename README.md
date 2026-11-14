# garmlink.ai — your Garmin data in Claude, ChatGPT and other AI assistants

[garmlink.ai](https://garmlink.ai) is a **hosted, read-only remote MCP server** for Garmin Connect. You sign in to Garmin once, garmlink syncs your history (activities, sleep, HRV, Body Battery, Training Readiness, VO2max, race predictions…), and any assistant that accepts a remote MCP connector can answer questions about it.

> This repository holds the public documentation and ready-to-paste client configurations. The service itself is closed-source and runs at `https://api.garmlink.ai/mcp`; nothing here needs to be installed or run.
>
> Not to be confused with other projects named "garmlink" that you install yourself: this one is the hosted service at garmlink.ai.

## Connect it

1. Create a free account at [garmlink.ai](https://garmlink.ai) and connect Garmin Connect from the dashboard.
2. Add the connector address to your assistant: `https://api.garmlink.ai/mcp`
3. Sign in when the assistant asks (OAuth), then ask a question.

| Assistant | How | Step-by-step guide |
|---|---|---|
| Claude | Custom connector — works on Claude's free plan too | [setup-claude](https://garmlink.ai/help/setup-claude) |
| ChatGPT | Developer mode — Plus, Pro, Business, Enterprise or Education, on the web | [setup-chatgpt](https://garmlink.ai/help/setup-chatgpt) |
| Perplexity | Custom remote connector — Pro, Max or Enterprise | [setup-perplexity](https://garmlink.ai/help/setup-perplexity) |
| Gemini | Custom apps in the Gemini app (US for now), the Gemini CLI or Enterprise | [setup-gemini](https://garmlink.ai/help/setup-gemini) |
| Le Chat (Mistral) | Custom MCP connector, added on the web — free plan included | [setup-le-chat](https://garmlink.ai/help/setup-le-chat) |
| Grok | Custom connector on grok.com, from the web | [setup-grok](https://garmlink.ai/help/setup-grok) |
| Cursor | [`configs/cursor.json`](configs/cursor.json) → `~/.cursor/mcp.json` | [setup-cursor](https://garmlink.ai/help/setup-cursor) |
| VS Code (GitHub Copilot, Agent mode) | [`configs/vscode.json`](configs/vscode.json) → `.vscode/mcp.json` | [setup-vscode](https://garmlink.ai/help/setup-vscode) |
| Windsurf | [`configs/windsurf.json`](configs/windsurf.json) → `~/.codeium/windsurf/mcp_config.json` | [setup-windsurf](https://garmlink.ai/help/setup-windsurf) |
| Antigravity | [`configs/antigravity.json`](configs/antigravity.json) → `~/.gemini/config/mcp_config.json`; sign in by pasting a code back | [setup-antigravity](https://garmlink.ai/help/setup-antigravity) |
| Claude Code | [`configs/claude-code.sh`](configs/claude-code.sh) | [setup-claude-code](https://garmlink.ai/help/setup-claude-code) |
| Codex | [`configs/codex.sh`](configs/codex.sh), or the app's MCP settings | [setup-codex](https://garmlink.ai/help/setup-codex) |

Any other client that can add a remote MCP server over Streamable HTTP with OAuth works the same way.

The site and every guide are also available in [French](https://garmlink.ai/fr), [German](https://garmlink.ai/de), [Spanish](https://garmlink.ai/es) and [Italian](https://garmlink.ai/it).

## What the assistant can read

48 tools, 6 prompts and 4 resources; the full reference is at [garmlink.ai/docs/mcp](https://garmlink.ai/docs/mcp) and the machine-readable manifest at [api.garmlink.ai/manifest.json](https://api.garmlink.ai/manifest.json).

- **Activities and training sessions** — `garmlink_activities_list`, `garmlink_activity_get`, `garmlink_activities_get`, `garmlink_activity_timeseries`, `garmlink_activity_gpx`, `garmlink_session_analysis`, `garmlink_exercise_sets_get`, `garmlink_stats_summary`, `garmlink_weekly_totals_get`
- **Sleep, recovery and daily health** — `garmlink_sleep_get`, `garmlink_hrv_get`, `garmlink_stress_get`, `garmlink_body_battery_get`, `garmlink_readiness_get`, `garmlink_heart_rate_get`, `garmlink_respiration_get`, `garmlink_spo2_get`, `garmlink_daily_summary_get`, `garmlink_daily_metric_get`, `garmlink_steps_get`, `garmlink_floors_get`, `garmlink_intensity_minutes_get`, `garmlink_hydration_get`, `garmlink_blood_pressure_get`, `garmlink_nutrition_get`, `garmlink_menstrual_get`
- **Fitness and performance** — `garmlink_training_status_get`, `garmlink_vo2max_history`, `garmlink_fitness_age_get`, `garmlink_race_predictions_get`, `garmlink_endurance_score_get`, `garmlink_hill_score_get`, `garmlink_lactate_threshold_get`, `garmlink_running_tolerance_get`, `garmlink_personal_records_get`, `garmlink_zones_get`
- **Body, gear and account** — `garmlink_body_composition_get`, `garmlink_weigh_ins_get`, `garmlink_gear_list`, `garmlink_devices_list`, `garmlink_profile_get`, `garmlink_solar_get`, `garmlink_golf_summary_get`, `garmlink_badges_get`, `garmlink_goals_get`, `garmlink_snapshot_get`
- **Sync** — `garmlink_sync_status`, `garmlink_sync_refresh`

Every tool reads. The only one that contacts Garmin on demand is `garmlink_sync_refresh`, which asks garmlink to fetch your latest data, at most once every 15 minutes. garmlink never writes to your Garmin account.

## Privacy

- Your Garmin password is used once to sign in and is never stored; garmlink keeps only the access tokens Garmin returns, encrypted.
- An assistant sees your data only when it calls a garmlink tool, and only while you keep it connected.
- The coach built into the dashboard, and the report emails if you turn them on, send the data they need to the AI providers named in the privacy policy.
- garmlink does not train any model on your data and does not sell it.
- Disconnecting Garmin in the dashboard stops the sync and deletes your synced data; deleting your account removes everything. Details: [privacy policy](https://garmlink.ai/privacy).

## Honest limits

- **Not an official Garmin partner.** garmlink signs in to Garmin Connect as you, with your consent; it does not use Garmin's partner Health API. If you want official access, see the comparison at [garmlink.ai/garmin-ai-connectors](https://garmlink.ai/garmin-ai-connectors).
- **Read-only.** It cannot send workouts or training plans to your watch.
- Garmin can change its sign-in at any time; when it does, a sync can pause until garmlink adapts.

## Compared with other options

- [Every way to connect Garmin to an AI assistant](https://garmlink.ai/garmin-ai-connectors)
- [Hosted vs installing a Garmin MCP server yourself](https://garmlink.ai/garmin-mcp-server)
- [garmlink or Tredict](https://garmlink.ai/alternatives/tredict)
- [garmlink or Fitness AI Connector](https://garmlink.ai/alternatives/fitness-ai-connector)
- [garmlink or Garmin Chat Connector](https://garmlink.ai/alternatives/garmin-chat-connector)

## Also listed on

- Official MCP Registry: `ai.garmlink/garmlink`
- [Glama](https://glama.ai/mcp/connectors/ai.garmlink.api/garmlink)

## Support

support@garmlink.ai · Garmin is a trademark of Garmin Ltd.; garmlink is independent and not affiliated with or endorsed by Garmin.
