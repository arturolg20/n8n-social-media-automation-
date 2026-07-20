# n8n Social Media Automation

AI-powered content generation, review and publishing workflows built with n8n, OpenAI, WordPress REST API and webhooks.

This repository contains modular n8n workflows designed to work together as the automation backend of a custom web application.

---

# Project Context

These workflows are not intended to be used as standalone automations.

They were designed as the backend automation layer of a custom web application where users can generate, review and publish AI-powered content through a graphical interface.

The web application collects all publication settings, such as:

- Language
- Tone
- Target audience
- Platform-specific options
- SEO information
- Image preferences

and sends them to the appropriate workflow through webhooks.

The automation then:

- Generates AI-powered content.
- Generates AI images.
- Uploads the generated image to the WordPress Media Library.
- Uses the uploaded WordPress media as the canonical image for every supported social media platform.
- Creates platform-specific content.
- Stores review sessions inside n8n Data Tables.
- Allows regenerating text or images before publication.
- Publishes approved content (Workflow 3).

This architecture avoids generating duplicate images for every platform while ensuring that every social network references the same media asset.

The frontend application is developed separately and communicates with these workflows through webhooks.

---

# Current Workflows

## Workflow 1 — Content Generation

Responsible for generating complete multi-platform content.

Main responsibilities:

- Generate AI content
- Generate AI image
- Upload image to WordPress
- Generate platform-specific versions
- Store draft into Data Table
- Create review session

File:

```
workflow-1-content-generation.json
```

---

## Workflow 2 — Review & Regeneration

Loads a previously generated draft and allows regenerating either the text or the image while preserving version history.

Main responsibilities:

- Load review session
- Regenerate article
- Regenerate image
- Preserve previous versions
- Update Data Table
- Return updated content

File:

```
workflow-2-review-regeneration.json
```

---

## Workflow 3 — Publishing

Coming soon.

Responsible for publishing approved content to WordPress and supported social media platforms.

---

# Overall Architecture

```text
                 Custom Web Application
                           │
                           ▼
                 Workflow 1
          AI Content Generation
                           │
                           ▼
            Draft stored in Data Table
                           │
                           ▼
                 Workflow 2
         Review & Regeneration
                           │
                           ▼
                Approved Draft
                           │
                           ▼
                 Workflow 3
          Publishing & Distribution
```

---

# Technologies

- n8n
- OpenAI
- Pollinations AI
- WordPress REST API
- n8n Data Tables
- Webhooks
- JavaScript (Code Nodes)

---

# Required Configuration

Before running the workflows configure:

## OpenAI

Create your own OpenAI credentials and assign them to every Chat Model node.

## WordPress

Replace the placeholder endpoints:

```
https://example.com/wp-json/...
```

with your own WordPress REST API endpoints.

Configure authentication for every WordPress node.

## Data Tables

Create a Data Table named:

```
content_sessions
```

and select it inside the required Data Table nodes.

---

# Repository Structure

```text
n8n-social-media-automation/

├── README.md
├── workflow-1-content-generation.json
├── workflow-2-review-regeneration.json
├── screenshots/
└── docs/
```

---

# Workflow Dependencies

The workflows are designed to work together.

Workflow 1 creates the review session.

Workflow 2 loads that session and allows regenerating text or images while preserving version history.

Workflow 3 will publish the approved content to WordPress and the configured social media platforms.

---

# System Design

The workflows are intentionally separated into independent modules.

This architecture provides several advantages:

- Easier maintenance
- Better scalability
- Independent testing
- Clear separation of responsibilities
- Reusable automation components

The custom frontend orchestrates the complete process by communicating with each workflow through dedicated webhooks.

---

# Roadmap

## Completed

- Workflow 1 — AI Content Generation
- Workflow 2 — Review & Regeneration

## In Progress

- Workflow 3 — Publishing & Distribution

---

# Notes

These workflows are provided as reusable templates.

Before running them you must configure:

- OpenAI credentials
- WordPress credentials
- Webhook URLs
- Data Tables
- Environment-specific settings

---

# License

MIT
