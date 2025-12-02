# 🏭 AI Prompt Factory: Web Application

This repository contains the **"Prompt Factory"** strategy designed to generate a production-grade, high-performance web application environment.

Instead of writing code manually, we use a **Two-Phase Prompting Strategy** to instruct an AI to act as a Senior Architect and generate the perfect implementation plan.

---

## 🚀 How to Use This Strategy

To generate the full source code and project structure, follow these steps in your AI Chat Interface:

### 1️⃣ Step 1: Initialize the Architect (Phase 1)
Copy the **Master Template** below and paste it as your **first message** to the AI. This sets the persona and the rules.

### 2️⃣ Step 2: Provide Configuration (Phase 2)
Once the AI acknowledges the first prompt (e.g., *"I am ready, please send the JSON"*), copy and paste the **JSON Configuration** block.

### 3️⃣ Step 3: Generation & Coding
The AI will output a massive, detailed "Final Developer Prompt". 
1. **Copy** that final output.
2. Open a **New Chat**.
3. **Paste** the final prompt to start the actual coding process.

---

## 📝 Phase 1: The Master Template

```
# ROLES & OBJECTIVE
You are a Senior Software Architect with 20+ years of experience and an Expert Prompt Engineer.
Your Goal: Analyze the "PROJECT CONFIGURATION JSON" I will provide below and generate an "Ultra-Detailed Development Prompt" that I can feed to another AI (The Developer Bot) to write the actual code.

# INPUT FORMAT
I will provide a JSON object containing:
- `project_meta`: Project goal and description.
- `tech_stack`: Languages, frameworks, databases, etc.
- `architecture`: Architectural patterns (e.g., Hexagonal, Clean Arch).
- `features`: Detailed breakdown of required modules.
- `requirements`: Security, Performance, URL strategies, Testing, etc.
- `exclusions`: Features strictly NOT needed.

# OUTPUT GENERATION RULES (How to construct the Final Prompt)
The output you generate must be the "Final Prompt" intended for a coding session. This Final Prompt must include:

1.  **System Identity:** Define the Developer Bot's role (e.g., "You are a World-Class NestJS Expert...").
2.  **Project Goal:** Clearly articulate the objective derived from the JSON.
3.  **Tech Stack (Strict Mode):** Command the bot to strictly follow the specified stack.
4.  **Architectural Guidelines:** Define folder structures, naming conventions, and patterns (e.g., separating `domain`, `application`, and `infrastructure` layers).
5.  **Module Breakdown:** List every module (User, Product, Order, etc.) with technical implementation details.
6.  **URL & Routing Strategy:** Explicitly define the routing rules—especially if there is a distinction between clean Backend APIs and complex/parameter-heavy Frontend simulation URLs.
7.  **Mocking & External Services:** Explain how to abstract and mock external dependencies (Payment, Shipping, etc.).
8.  **Data & Seeding:** Instructions for creating a robust CLI seeder for Big Data simulation.
9.  **DevOps & Environment:** Strict rules against hardcoding ports/URLs. Enforce Docker and Environment Variable usage.
10. **Deliverables:** Define the expected output format (File structure, Complete Code blocks, Swagger docs, Docker-compose).

# WAIT MODE
For now, only understand these instructions and acknowledge by saying: "Please send the Project Configuration JSON data. I am ready to architect the system." Do not generate anything else yet.
```



### Phase 2 Sample

<details>
  <summary>🔽 This is an example for an e-commerce application</summary>

  ```json
{
  "project_meta": {
    "name": "E-Commerce Load Test Environment",
    "description": "A high-performance backend environment mimicking a real e-commerce site, designed for high-volume data generation, load testing, tool testing. It serves as a robust target for security scanners.",
    "primary_goal": "To provide a stable, data-rich environment for testing security scanners and simulating high-traffic scenarios."
  },
  "tech_stack": {
    "language": "TypeScript",
    "framework": "NestJS",
    "architecture": "Hexagonal / Clean Architecture (Domain-Driven Design principles)",
    "database": "PostgreSQL (include partitioning strategies for big data)",
    "orm": "Prisma OR TypeORM (Default to Prisma)",
    "caching_queue": "Redis (Session caching, Rate limiting, Queues)",
    "auth": "OAuth2 (Authorization Code + PKCE) + JWT (Stateless)",
    "validation": "class-validator, class-transformer",
    "documentation": "OpenAPI / Swagger (Auto-generated)",
    "testing": "Jest (Unit), k6 (Load), Supertest (Integration)"
  },
  "features": [
    {
      "module": "User System",
      "details": ["Register/Login", "Email Verify (Mock mechanism)", "Password Reset", "Role Management (User, Admin, Support, Courier)", "OAuth2 Token Refresh"]
    },
    {
      "module": "Product System",
      "details": ["Category Tree", "Product CRUD", "Inventory Management", "Multi-image support (Mock storage)", "Variant Management (Color, Size, etc.)"]
    },
    {
      "module": "Cart & Order System",
      "details": ["Add/Remove Cart", "Checkout Simulation", "Mock Payment (Success/Fail/3DS scenarios)", "Order State Machine (Pending->Paid->Shipped->Delivered->Return)"]
    },
    {
      "module": "Review & Report System",
      "details": ["Submit Review", "Like Review", "Report Review (Moderation flow)", "Admin Moderation API"]
    },
    {
      "module": "Mock Integrations",
      "details": ["Mock Payment Gateway (Sandbox)", "Mock Shipping Provider (Tracking Codes/Status updates)", "Mock SMS/Email Service (Log content to console/file)"]
    },
    {
      "module": "Admin Panel API",
      "details": ["User Management", "Order Overview", "Sales Reports", "System Logs Access", "Data Reset Button"]
    }
  ],
  "requirements": {
    "url_strategy": {
      "backend_api": "Short, clean, RESTful (e.g., /api/v1/products/:id)",
      "frontend_simulation": "Must support the generation/handling of complex, long, parametric URLs to facilitate DAST crawling. (e.g., /products/laptop?model=pro&ref=banner&session=xyz&tracking=123&utm_source=google&utm_campaign=spring2025)",
      "rewrite_rules": "The backend must gracefully handle or ignore extra/marketing query parameters without throwing errors."
    },
    "security": {
      "focus": "Standard security (CSRF, XSS filters, SQLi protection) BUT configurable to facilitate testing.",
      "rate_limiting": "Must be Flexible/Configurable via ENV. Do NOT aggressively block DAST scanners by default.",
      "sensitive_data": "Do not log PII (Personal Identifiable Information), but log the request/response flow for debugging."
    },
    "data_generation": {
      "type": "Heavy / Big Data",
      "seed_script": "CLI based (e.g., `npm run seed:large`). Capable of generating 1M+ products, 5M+ reviews, and realistic user history.",
      "randomization": "Use `faker.js` for realistic data, distributed categories, and realistic order history simulation."
    },
    "devops": {
      "containerization": "Docker + Docker Compose",
      "configuration": "All ports, DB credentials, and secrets must be in `.env`. NO HARDCODED PORTS or URLS.",
      "services": "Application, PostgreSQL, Redis"
    }
  },
  "exclusions": [
    "APM Hooks (ElasticAPM, OpenTelemetry) - Keep it simple",
    "Complex CI/CD Pipelines (GitHub Actions/GitLab CI yaml files) - Focus on local Docker execution",
    "Strict IP-based blocking (Must be disabled or easily adjustable for DAST scanning)"
  ]
}
