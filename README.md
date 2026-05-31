# MeetingBuddy

MeetingBuddy is a Microsoft Copilot Studio agent that turns a meeting transcript into completed post-meeting follow-up work.

After a meeting, organisers usually spend time writing minutes, extracting action items, creating Planner tasks, sending follow-up emails, and saving documents. MeetingBuddy reduces that admin work by analysing the transcript, preparing the follow-up plan, asking for one confirmation, and then executing the work across Microsoft 365.

## What MeetingBuddy Does

- Analyses a meeting transcript.
- Detects the meeting type:
  - Internal Standup
  - Stakeholder Exploration
  - General Meeting
- Selects the right minutes template.
- Suggests the correct SharePoint folder.
- Generates meeting minutes.
- Prepares Planner follow-up tasks.
- Drafts a follow-up email.
- Suggests follow-up meeting details when needed.
- Asks for organiser confirmation before taking action.
- Saves minutes to SharePoint.
- Sends an Outlook follow-up email.
- Creates and updates a Planner task.
- Posts a Teams acknowledgement.
- Schedules a follow-up Outlook calendar invite when requested.
- Returns a completion acknowledgement.

## Microsoft Technologies Used

- Microsoft Copilot Studio
- Copilot Studio topics
- Copilot Studio custom prompt
- Copilot Studio agent flow
- SharePoint Online
- Office 365 Outlook
- Microsoft Planner
- Microsoft Teams
- Outlook Calendar

## Demo Trigger

For the hackathon demo, the transcript is pasted manually into the Copilot Studio test chat.

In the production design, MeetingBuddy would trigger automatically when a Microsoft Teams transcript becomes available after a meeting ends. That production trigger depends on tenant-level transcript access, Microsoft Graph/API permissions, and admin configuration, so the demo focuses on the working agent reasoning and Microsoft 365 execution path.

## Demo Flow

```text
User provides meeting transcript
MeetingBuddy analyses transcript
MeetingBuddy detects meeting type
MeetingBuddy prepares minutes, tasks, email, and follow-up plan
Organiser confirms
Agent flow creates SharePoint file
Agent flow sends Outlook email
Agent flow creates and updates Planner task
Agent flow posts Teams acknowledgement
Agent flow schedules follow-up meeting when requested
MeetingBuddy returns acknowledgement
```

## Repository Contents

```text
README.md
architecture.md
agent-instructions.md
prompt.md
setup.md
demo-transcript.md
submission-draft.md
technical-notes.md
screenshots/
assets/
```

## Current MVP Scope

The working MVP demonstrates the core Operative-track pattern:

- Prompt reasoning over meeting content.
- Human review and confirmation.
- Agent flow orchestration.
- Microsoft 365 connected actions.
- Real outputs in Outlook, Planner, and SharePoint.
- Teams acknowledgement post.
- Optional Outlook calendar invite.

## Future Enhancements

- Automatic Teams transcript trigger using Microsoft Graph.
- Full Teams Adaptive Card review and editing experience.
- One Planner task per extracted action item.
- Duplicate-safe Planner task checking.
- Outlook calendar availability lookup for follow-up scheduling.
- Word `.docx` minutes generation from a formal template.
- Sentiment and concern detection for stakeholder meetings.
