---
Title: "Signal 11: Calendar-Grade Automation Precision"
Tags:
  - #prompt-technique
  - #automation
  - #agentic-ai
---

# Signal 11: Calendar-Grade Automation Precision

This signal indicates that when creating automations, GPT-5 expects highly specific, standardized formats for scheduling.

## The Signal

> "Schedules must be given in iCal VEVENT format... Prefer the RRULE: property whenever possible."

## So What?

Automation requests require enterprise-level specificity. Vague timing instructions (e.g., "run this every week") will result in the system using its own defaults, which may not match your actual intent.

## How to Use It (Exploit)

Always specify the timezone and use a precise recurrence rule (RRULE) when defining a schedule for an automation.

### Example:

```
Task: Send a weekly summary email.
Schedule: Weekly Monday 9 AM Pacific: RRULE:FREQ=WEEKLY;BYDAY=MO;BYHOUR=9;BYMINUTE=0;TZID=America/Los_Angeles
```

---

[[../../1-Notes/projects/business/bx-os/nate-jones-article-synthesis-hub.md|Back to Synthesis Hub]]
