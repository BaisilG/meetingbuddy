# Setup Guide

This project is built in Microsoft Copilot Studio using a topic, a custom prompt, and an agent flow.

## Prerequisites

- Microsoft Copilot Studio environment.
- Access to SharePoint Online.
- Access to Office 365 Outlook.
- Access to Microsoft Planner.
- A SharePoint site for MeetingBuddy output.
- A Planner plan for MeetingBuddy tasks.

## 1. Create The Agent

Create a Copilot Studio agent named:

--------
MeetingBuddy
--------

Paste the instructions from `agent-instructions.md` into the agent instructions area.

## 2. Create The Topic

Create a topic named:

--------
Process Meeting Transcript
--------

Topic description:

--------
Use this topic when the user wants to process a meeting transcript, generate meeting minutes, extract action items, prepare follow-up emails, schedule a follow-up meeting, and confirm post-meeting actions.
--------

Add a question:

--------
Please paste the full meeting transcript. Include the meeting title, date, and attendee names/emails if available.
--------

Save the response as:

--------
meetingTranscript
--------

## 3. Add The Prompt

Create a prompt named:

--------
Analyse Meeting Transcript
--------

Use the prompt from `prompt.md`.

Map:

--------
meetingTranscript = meetingTranscript
--------

Save the prompt output as:

--------
meetingAnalysisResult
--------

Display:

--------
meetingAnalysisResult.text
--------

Set a topic variable:

--------
analysisText = meetingAnalysisResult.text
--------

## 4. Add Confirmation

Add a multiple-choice confirmation question:

--------
Do you want me to execute these follow-up actions now?
--------

Options:

--------
Confirm
Cancel
--------

Save as:

--------
confirmationChoice
--------

## 5. Create Agent Flow

Create an agent flow named:

--------
Execute MeetingBuddy Follow Up
--------

Trigger:

--------
When an agent calls the flow
--------

Inputs:

--------
meetingAnalysis
meetingTranscript
recipientEmail
scheduleFollowUp
followUpStartTime
--------

Actions:

1. SharePoint - Create file.
2. Compose or HTML Template action for formatted content.
3. Office 365 Outlook - Send an email (V2).
4. Planner - Create a task.
5. Planner - Update task details.
6. Office 365 Outlook - Create event when follow-up scheduling is requested.
7. Teams - Post message in a chat or channel.
8. Respond to the agent.

## 6. Recommended Flow Mapping

SharePoint:

--------
File Name: MeetingBuddy-Minutes.html
File Content: formatted HTML containing meetingAnalysis
--------

Outlook:

--------
To: recipientEmail
Subject: MeetingBuddy Follow-Up Summary
Body: formatted HTML containing meetingAnalysis
--------

Planner:

--------
Title: Review MeetingBuddy follow-up actions
Bucket: Up next
Task details/description: meetingAnalysis
--------

Calendar:

--------
Condition: scheduleFollowUp is equal to Yes
Subject: MeetingBuddy Follow-up Meeting
Start Time: confirmed demo follow-up time
End Time: confirmed demo follow-up end time
Time Zone: Dublin, Edinburgh, Lisbon, London
Required Attendees: recipientEmail
Body: meetingAnalysis
--------

Teams:

--------
Post in: Channel
Message: short MeetingBuddy completion acknowledgement
--------

Respond to agent:

--------
Completed. I created the meeting minutes file in SharePoint, sent the follow-up email, created and updated a Planner task, posted a Teams acknowledgement, and scheduled the follow-up meeting if requested.
--------

## 7. Connect Topic To Flow

In the Confirm branch, call:

--------
Execute MeetingBuddy Follow Up
--------

Map:

--------
meetingAnalysis = analysisText
meetingTranscript = meetingTranscript
recipientEmail = your demo email address
scheduleFollowUp = scheduleFollowUp converted to Yes or No text
followUpStartTime = followUpStartTimeText
--------

In the Cancel branch, send:

--------
No problem. I will not create any files, tasks, emails, or meeting invites.
--------

## 8. Test

Start a new test session and type:

--------
Process this meeting
--------

Paste the transcript from `demo-transcript.md`.

Expected outputs:

- Stakeholder Exploration classification.
- Meeting minutes generated.
- Planner tasks proposed.
- Follow-up email drafted.
- Confirm/Cancel shown.
- On Confirm, SharePoint file created, Outlook email sent, Planner task created.
- Teams acknowledgement posted.
- Follow-up meeting invite created when scheduling is selected.
