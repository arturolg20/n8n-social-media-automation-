# n8n-social-media-automation-
AI-powered social media content generation and publishing automation built with n8n, APIs and webhooks.

# AI Social Media Content Generation Workflow (Workflow 1)

## Overview

This n8n workflow automates the generation of AI-powered social media content and prepares it for review before publication.

Instead of publishing content directly, the workflow creates a complete draft, generates an accompanying image, organizes platform-specific versions, and stores everything in a Data Table for later review or approval.

This workflow is designed to be the first step of a larger three-workflow automation system.

---

## Features

- Receives requests through a Webhook
- Generates AI-powered content
- Creates AI-generated images
- Validates article length
- Automatically retries generation if validation fails
- Creates WordPress categories when needed
- Creates WordPress tags automatically
- Generates platform-specific versions:
  - WordPress
  - LinkedIn
  - X (Twitter)
  - Facebook
  - Instagram
- Stores every generated draft in an n8n Data Table
- Returns the generated content through the webhook response

---

## Workflow Architecture

Webhook
↓

Input Mapping
↓

AI Content Generation
↓

Content Validation
↓

Generate AI Image
↓

Create Category (if needed)
↓

Create Tags

↓

Merge Content + Image
↓

Prepare Review Data
↓

Save Draft into Data Table
↓

Webhook Response

---

## Technologies

- n8n
- OpenAI
- Pollinations AI
- WordPress REST API
- n8n Data Tables
- Webhooks
- JavaScript (Code Nodes)

---

## Required Configuration

Before running the workflow, configure:

### OpenAI

Create an OpenAI credential and assign it to all Chat Model nodes.

### WordPress

Replace the placeholder endpoints:

```
https://example.com/wp-json/...
```

with your own WordPress REST API endpoints.

Configure authentication for:

- Upload Image
- Create Category
- Create Tag

### Data Table

Create a Data Table named:

```
content_sessions
```

and select it in the **Insert Row** node.

---

## Example Webhook Request

POST

```json
{
  "titulo": "Benefits of AI Automation",
  "descripcion": "Generate an article about AI automation.",
  "category": "Artificial Intelligence",
  "tags": "AI,Automation,n8n",
  "idioma": "English",
  "tamano": "Medium",
  "tono": "Professional",
  "publication_type": "Blog"
}
```

---

## Example Response

```json
{
  "success": true,
  "session_id": "xxxxx",
  "status": "pending_review",
  "title": "...",
  "content": "...",
  "image": "...",
  "category": "...",
  "tags": [...]
}
```

---

## Repository Structure

```
workflow-1-content-generation.json
README.md
screenshots/
```

---

## Future Work

This repository contains only **Workflow 1**.

The complete automation is divided into three independent workflows:

- Workflow 1 — AI Content Generation
- Workflow 2 — Review & Regeneration
- Workflow 3 — Publishing & Distribution

---

## License

MIT
