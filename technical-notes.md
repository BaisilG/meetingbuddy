# Technical Notes

## Design Pattern

MeetingBuddy separates planning from execution.

```text
Prompt = analyse transcript and prepare the plan
Topic = show plan and ask for confirmation
Agent flow = execute Microsoft 365 actions
```

This keeps the agent safer because no external actions run until the organiser confirms.

## Important Variable Flow

The custom prompt output is returned as a record. The text field must be mapped into a topic variable before passing it to the agent flow.

```text
meetingAnalysisResult.text -> analysisText -> meetingAnalysis flow input
```

This prevents the flow from receiving a literal string such as `meetingAnalysisResult.text`.

## Safety Notes

- The prompt is instructed not to claim actions have been completed.
- The topic handles the Confirm/Cancel step.
- The flow performs the real actions only after confirmation.
- The prompt is instructed not to invent names, emails, dates, deadlines, or task owners.

## Current Demo Limitation

The demo uses manual transcript input in the Copilot Studio test chat.

In production, the transcript would be passed into MeetingBuddy automatically when a Microsoft Teams meeting transcript becomes available. That requires tenant-level transcript access, Microsoft Graph/API permissions, and admin configuration.

## MVP vs Production

Current MVP:

- One generated meeting analysis.
- One formatted SharePoint minutes file.
- One formatted Outlook follow-up email.
- One Planner follow-up task updated with the generated analysis.
- One Teams acknowledgement post.
- Optional Outlook calendar invite for the confirmed follow-up meeting.

Production enhancements:

- One Planner task per extracted action item.
- Duplicate checking against existing Planner tasks.
- Calendar availability lookup.
- Teams Adaptive Card review.
- Word template `.docx` generation.
- Automatic Teams transcript trigger.
