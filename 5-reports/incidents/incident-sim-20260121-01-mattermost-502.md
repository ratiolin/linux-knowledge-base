## Incident Summary

- System: Mattermost (prod)
- Symptom: Web returns 502 Bad Gateway
- Impact: All users unable to access chat UI
- Severity: SEV-2 (full outage, no data loss)
- Duration: ~12 minutes
## Timeline

- T0 
  User reports "Chat page shows 502 Bad Gateway"

- T1 
  Initial check: access https://chat.metratio.com → confirmed 502

- T2   
  Checked container status: all containers running

- T3 
  Reviewed nginx logs, observed upstream connection failure

- T4 
  Identified incorrect upstream port in nginx config

- T5  
  Reverted upstream port and reloaded nginx

- T6 
  Service restored, user access verified
## Hypotheses & Elimination

| Hypothesis | Reason | Action | Result |
|-----------|------|------|------|
| Mattermost container down | Common cause of 502 | docker compose ps | Rejected |
| Database unavailable | Backend dependency | Container logs | Rejected |
| Nginx misconfiguration | Recent change risk | Inspect nginx config | Confirmed |
## Decision Rationale

Upstream configuration rollback was chosen because:

- Change was isolated to nginx config
- No data impact risk
- Reload is non-destructive
- Rollback path was clear and immediate
## Recovery Verification

- HTTP 200 returned from chat.metratio.com
- User login successful
- Message send confirmed
## Improvements

- Enforce staging verification before nginx config changes
- Add simple HTTP health check for upstream
- Require change record for proxy-level changes
