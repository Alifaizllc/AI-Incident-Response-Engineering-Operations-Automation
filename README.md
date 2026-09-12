🚨 AI Incident Response & Engineering Operations Automation

This repository contains an AI-powered incident response and engineering operations automation system built with n8n.

The workflow automatically receives production incidents, analyzes severity and category with AI, detects duplicates, retrieves relevant engineering runbooks using RAG, checks service health, creates GitHub issues, sends alerts, monitors SLA windows, escalates unresolved incidents, and generates AI-powered postmortems after resolution.

🖼️ Workflow Overview

<img width="959" height="409" alt="AI Incident Response Workflow" src="https://github.com/user-attachments/assets/a3c5a4f2-577a-42f5-b1da-d8bd596fa6fc" />

Webhook
   ↓
Normalize Incident
   ↓
AI Triage
   ↓
Duplicate Detection
   ↓
Supabase Incident Tracking
   ↓
AI Investigator + RAG
   ↓
Service Health Check
   ↓
GitHub Issue Creation
   ↓
Severity-Based Gmail Alert
   ↓
SLA Wait
   ↓
GitHub Issue Status Check
   ↓
 ┌───────────────────────────────┐
 │ Issue Still Open              │ Issue Resolved
 │ ↓                             │ ↓
 │ Escalation                    │ AI Postmortem
 │ ↓                             │ ↓
 │ Supabase Update               │ Supabase Update
 │ ↓                             │ ↓
 │ Gmail Escalation Alert        │ Resolution Email
 └───────────────────────────────┘

🧠 How It Works

The system automates the complete incident-response lifecycle from incident intake to resolution.

1️⃣ Receive Incident

Receives production incidents through an n8n Webhook

Accepts incident details such as:

Title

Description

Service

Service URL

Source

Normalizes the incoming payload before processing

2️⃣ AI Triage

Uses an LLM to analyze the incident

Determines:

Severity

Category

Responsible team

AI-generated summary

Probable cause

Recommended action

Converts raw monitoring data into structured incident information

3️⃣ Duplicate Detection

Checks Supabase for similar or existing incidents

Prevents unnecessary duplicate incident creation

Updates duplicate count and tracking information when required

4️⃣ Incident Tracking with Supabase

Stores incident information in Supabase / PostgreSQL

Tracks:

Status

Severity

Category

Team

GitHub issue

Duplicate count

Timestamps

Escalation state

Postmortem

5️⃣ AI Investigator + RAG

Retrieves relevant engineering runbooks using RAG

Uses vector search to find the most relevant troubleshooting guidance

Helps the AI investigator generate better incident analysis and recommended actions

Example runbook categories:

Authentication Service

Database Incident

API Downtime

Deployment Failure

High Latency / Performance

Security Incident

6️⃣ Service Health Check

Sends an HTTP request to the affected service

Checks:

Reachability

HTTP status code

Service health

Adds service-health context to the incident investigation

7️⃣ GitHub Issue Automation

Automatically creates a GitHub issue for new incidents

Includes relevant incident context for the engineering team

Stores the GitHub issue number and URL in Supabase

8️⃣ Severity-Based Alerts

Sends incident notifications through Gmail

Alert content depends on incident severity

Helps engineering teams quickly identify high-priority incidents

9️⃣ SLA Monitoring

Waits for the configured SLA window

Checks the GitHub issue status after the SLA period

Determines whether the incident is still open or resolved

🔟 Escalation or Resolution

If the Incident Is Still Open

Marks the incident as Escalated

Updates Supabase

Sends an escalation email

If the Incident Is Resolved

Generates an AI-powered postmortem

Updates the incident as resolved

Stores the postmortem in Supabase

Sends a resolution notification

🚀 Features

✅ AI-powered incident triage

✅ Severity and category classification

✅ Duplicate incident detection

✅ Supabase incident tracking

✅ RAG-based engineering runbook retrieval

✅ AI investigator workflow

✅ Automated service health checks

✅ Automatic GitHub issue creation

✅ Severity-based Gmail alerts

✅ SLA monitoring

✅ Automatic escalation

✅ AI-generated postmortems

✅ End-to-end engineering operations automation

🛠️ Technologies Used

Tool / Platform

Purpose

n8n

Workflow automation and orchestration

Groq LLMs

AI triage and incident investigation

Gemini Embeddings

Generate embeddings for RAG

Supabase

Incident database and vector storage

PostgreSQL

Structured incident data

pgvector

Vector similarity search

GitHub

Engineering issue tracking

Gmail

Incident, escalation, and resolution alerts

HTTP APIs

Service health checks and integrations

RAG

Engineering runbook retrieval

🗄️ Incident Data Model

The incident database stores information such as:

id
title
description
service
service_url
severity
category
team
status
ai_summary
probable_cause
recommended_action
fingerprint
duplicate_count
github_issue_number
github_issue_url
postmortem
created_at
last_seen_at
updated_at
resolved_at

📚 RAG Knowledge Base

The project uses engineering runbooks stored in Supabase.

RAG Flow

Incident
   ↓
Generate Query
   ↓
Gemini Embedding
   ↓
pgvector Similarity Search
   ↓
Relevant Engineering Runbook
   ↓
AI Investigator

This allows the AI investigator to use relevant engineering knowledge instead of relying only on the LLM's general knowledge.

🔧 Setup Guide

⚠️ Prerequisites

n8n Cloud or self-hosted n8n

Groq API credentials

Gemini API credentials

Supabase project

GitHub account / token

Gmail OAuth credentials

📥 Import Workflow into n8n

Download the workflow JSON file from this repository.

Open n8n.

Go to:

Workflows → Import from File

Select the workflow JSON file.

🔌 Configure Credentials in n8n

Create and configure your own credentials for:

Groq

Gemini

Supabase

GitHub

Gmail

🗃️ Configure Supabase

Create the required incident table and vector-enabled knowledge-base tables.

The RAG knowledge base should support:

Document storage

Embeddings

Vector similarity search

Runbook retrieval

📄 Add Engineering Runbooks

Add engineering runbooks to the knowledge base and generate embeddings.

Example categories:

Authentication Service
Database Incident
API Downtime
Deployment Failure
High Latency / Performance
Security Incident

🔐 Security

This repository does not require sharing private credentials.

Before publishing or importing an n8n workflow, make sure the workflow does not contain:

API keys

Passwords

OAuth tokens

Supabase service-role keys

Private webhook secrets

Gmail credentials

Always configure credentials securely inside n8n.

💡 Use Cases

This workflow can be adapted for:

SaaS production incident response

DevOps alert automation

Engineering operations

API monitoring

Internal IT incident management

Support escalation

AI-assisted root-cause investigation

Automated incident reporting

🎯 What This Project Demonstrates

AI Automation

AI Agents

Agentic Workflows

RAG

LLM Integration

API Integration

Webhooks

Workflow Orchestration

Vector Search

Database Integration

Incident Management

SLA Monitoring

Engineering Automation

AI-Assisted Operations

👤 Author

Developed by Ali Faiz
