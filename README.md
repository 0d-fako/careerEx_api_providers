# 🌱 Personal Wellness Tracker (n8n Workflow)

## Overview
The **Personal Wellness Tracker** is an automated workflow built in **n8n** that helps individuals reflect on their daily wellbeing. It captures check‑in data (mood, sleep, exercise, reflection), uses AI to provide empathetic feedback, and generates weekly reports for long‑term growth.

This workflow demonstrates how AI agents can be integrated into structured automation to deliver personalized, human‑centered support at scale.

---

## Workflow Steps

### 1. Trigger – Daily Check‑In
- **Node**: Google Sheets (On Row Added).
- **Fields Captured**:  
  - `Name`  
  - `Email`  
  - `Mood` (1–10 scale)  
  - `Sleep Hours`  
  - `Exercise` (Yes/No)  
  - `Reflection` (free text)  
  - `Date` (optional, for weekly reports)

### 2. AI Agent – Empathetic Reflection
- **Node**: Claude AI Agent.
- **System Prompt**:  
  *“You are a compassionate wellness coach. Analyze the user’s check‑in data. Provide encouragement, highlight positive patterns, and gently suggest improvements. Output structured JSON with {status, encouragement, suggestion}.”*
- **User Prompt**: Injects the daily check‑in values.
- **Output Example**:
  ```json
  {
    "status": "Needs Attention",
    "encouragement": "You're doing well by exercising regularly.",
    "suggestion": "Try to get at least 7 hours of sleep tonight."
  }

### 3. Branching Logic
- Healthy → Motivational email.
- Needs Attention → Email with practical tips.
- Critical → Alert email 


### 4. Weekly Report
- *Node*: Cron (runs every Sunday).
- *Action*: Reads all entries from the past week.
- *AI Node*: Summarizes weekly trends.
- *Email Node*: Sends the report to the user.