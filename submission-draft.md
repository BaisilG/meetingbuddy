# Agent Academy Hackathon Submission Draft

## Participation Track

Operative

## Project Name

MeetingBuddy

## Problem Statement

MeetingBuddy solves the post-meeting administration burden faced by teams after Microsoft Teams meetings. After every meeting, organisers often spend 30-90 minutes writing minutes, extracting action items, creating Planner tasks, sending follow-up emails, and saving documentation.

The target users are automation teams, project teams, managers, and meeting organisers who need a reliable way to turn meeting conversations into completed follow-up work.

MeetingBuddy uses Copilot Studio to analyse a meeting transcript, detect the meeting type, select the right minutes template and SharePoint folder, prepare Planner tasks, draft a follow-up email, and ask for organiser confirmation before executing Microsoft 365 actions.

Success means the organiser can move from transcript to saved minutes, sent email, Planner task, Teams acknowledgement, optional calendar invite, and final acknowledgement with one confirmation.

## Agent Academy Modules or Concepts Used

- Copilot Studio agent instructions - defined MeetingBuddy as a post-meeting automation assistant with safety rules and confirmation before action.
- Prompt integration - used a custom AI prompt to analyse meeting transcripts, classify meeting type, extract tasks, draft emails, and prepare follow-up details.
- Agent flows - used an agent flow to execute Microsoft 365 actions after confirmation.
- Tool/action orchestration - connected the agent to SharePoint, Outlook, Planner, Teams, and Outlook Calendar.
- Human-in-the-loop confirmation - prevented actions from running until the organiser reviewed and confirmed the generated follow-up plan.

## Architecture Overview

MeetingBuddy architecture:

1. User provides a Microsoft Teams meeting transcript in the Copilot Studio test chat.
2. In production, this input would be triggered automatically when a Teams transcript becomes available after a meeting ends.
3. Copilot Studio topic receives the transcript and passes it to a custom prompt.
4. The prompt analyses the transcript and returns meeting type, confidence score, minutes template, SharePoint folder suggestion, meeting minutes, Planner tasks, follow-up email draft, and follow-up meeting details.
5. The agent shows the generated plan to the organiser.
6. The organiser confirms or cancels.
7. After confirmation, the agent flow runs Microsoft 365 connected actions:
   - creates a SharePoint meeting minutes file
   - sends an Outlook follow-up email
   - creates a Planner follow-up task
   - updates Planner task details
   - posts a Teams acknowledgement
   - schedules a follow-up Outlook calendar invite when requested
   - returns a completion message
8. Copilot Studio acknowledges completion to the organiser.

Integration points:

- Microsoft Copilot Studio
- Custom prompt
- Agent flow
- SharePoint Online
- Office 365 Outlook
- Microsoft Planner
- Microsoft Teams
- Outlook Calendar

## Key Technologies Used

- Microsoft Copilot Studio
- Copilot Studio topics
- Copilot Studio custom prompts
- Copilot Studio agent flows
- Power Automate-style connected actions
- SharePoint Online
- Office 365 Outlook
- Microsoft Planner
- Microsoft Teams
- Outlook Calendar

## What Worked Well Using The Agent Academy Curriculum

The Operative concepts were the most useful because they helped structure MeetingBuddy as more than a basic chatbot. I applied prompt reasoning, agent flow orchestration, and human confirmation before action.

The curriculum helped me understand how to separate the agent brain from the execution layer: Copilot Studio analyses and coordinates the work, while connected actions perform the Microsoft 365 tasks.

## What Was Unclear Or Difficult In The Curriculum

The most challenging part was understanding how to pass generated prompt output correctly into agent flows and connected actions. It would be helpful to have more examples showing dynamic variable mapping between prompts, topics, and agent flows.

Another challenge was automatic Teams transcript triggering, which depends on tenant-level permissions and Microsoft Graph/API setup. For the demo, I used manual transcript input while documenting the production trigger.

## Quick Setup Summary

1. Open the MeetingBuddy solution in Microsoft Copilot Studio.
2. Review the MeetingBuddy agent instructions.
3. Open the Process Meeting Transcript topic.
4. Review the Analyse Meeting Transcript prompt.
5. Review the Execute MeetingBuddy Follow Up agent flow.
6. Connect SharePoint, Outlook, and Planner using Microsoft 365 credentials.
7. Run the agent in Copilot Studio test chat.
8. Type "Process this meeting" and paste the sample transcript.
9. Confirm execution to create the SharePoint minutes file, send the Outlook email, create/update the Planner task, post the Teams acknowledgement, and schedule the follow-up meeting if requested.

## Technical Highlights

- Built an Operative-style Copilot Studio agent that combines transcript reasoning with Microsoft 365 execution.
- Created a custom prompt to classify meeting type, select templates, suggest folders, extract tasks, draft emails, and prepare follow-up details.
- Implemented human-in-the-loop confirmation so no external action happens before organiser approval.
- Used an agent flow to orchestrate SharePoint, Outlook, Planner, Teams, and calendar actions.
- Improved output quality with formatted HTML email/minutes and safer prompt rules to avoid invented details.

## Challenges & Learnings

The biggest challenge was making sure the generated meeting analysis was passed into the flow as real dynamic content rather than plain text. I solved this by storing the prompt output in a topic variable and mapping that variable into the agent flow inputs.

I also learned the importance of separating planning from execution. The prompt should only prepare the plan, while the agent flow performs the actual Microsoft 365 actions after confirmation.
