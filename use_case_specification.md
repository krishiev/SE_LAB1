markdown
# Use-Case Flow Specification: Receive Expiry Alerts

**Use Case Name:** Receive Expiry Alerts  
**Primary Actor:** SysAdmin  
**Preconditions:**
- The domain or SSL endpoint is registered in the system.
- The daily automated scan engine has identified an asset expiring within the 30, 15, or 3-day window.

## Main Success Scenario
1. The automated scan engine identifies an SSL certificate expiring in 15 days.
2. The system generates an alert notification containing the domain name, expiration date, and days remaining.
3. The system dispatches the alert to the SysAdmin's configured contact channel (e.g., Email/Slack).
4. The SysAdmin receives the alert and logs into the system dashboard.
5. The SysAdmin marks the alert as "Acknowledged".

**Postconditions:**
- The alert status is updated to "Acknowledged" in the system log database.
- The escalation timer for this specific alert is stopped.

## Alternate Flow (Alert Escalation)
- **At Step 4 of Main Success Scenario:** If the SysAdmin does not acknowledge the alert within 24 hours:
  1. The system detects the expiration of the acknowledgment grace period.
  2. The system triggers the escalation ladder.
  3. The system routes the alert notification directly to the Security Officer.
  4. The Security Officer receives the escalated alert.