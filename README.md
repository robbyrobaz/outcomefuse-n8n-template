# OutcomeLimit n8n Loss Control

An importable n8n HTTP Request node for reporting a business outcome to [OutcomeLimit](https://web-production-b0715.up.railway.app).

n8n can report a successful execution even when the workflow produced an empty, stale, incomplete, or commercially harmful result. OutcomeLimit is an independent watcher for n8n agencies: it checks expected outcomes and cadence, records incident evidence, enforces rolling 24-hour and 7-day loss budgets, and can deactivate only an explicitly armed workflow through the official n8n API.

## Install

1. [Start a 14-day OutcomeLimit trial](https://web-production-b0715.up.railway.app/signup).
2. Connect an n8n instance and create an outcome contract.
3. Download or copy `outcomelimit-outcome-signal.json` into n8n.
4. Replace the monitor URL and one-time bearer token with the values shown in OutcomeLimit.
5. Place the node after the real business action, such as the CRM write or message delivery.

The template uses n8n's Continue on Error behavior. A temporary monitoring outage will not interrupt the protected business workflow.

## Payload

```json
{
  "outcome_ok": true,
  "result": { "records": 27 },
  "estimated_loss": 0
}
```

Set `outcome_ok` to `false` and include a `reason` when the business action fails. `estimated_loss` is accumulated against customer-defined daily and weekly limits. A missing signal is also detected by the external watcher.

## Safety

Automatic workflow deactivation is off by default. It must be armed separately for each monitor, and reactivation is manual. API credentials and alert webhook URLs are encrypted at rest.

Full documentation: [OutcomeLimit n8n setup guide](https://web-production-b0715.up.railway.app/docs)
