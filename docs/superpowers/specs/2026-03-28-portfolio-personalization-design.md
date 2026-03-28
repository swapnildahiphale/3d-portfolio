# Portfolio Personalization — Content Swap for Swapnil Dahiphale

**Date**: 2026-03-28
**Type**: Content replacement — no visual/structural changes
**Scope**: Replace all personal content from Akash Malhotra's portfolio with Swapnil Dahiphale's details

## Constraints

- Keep all animations, 3D character, layout, and styling exactly as-is
- Keep the carousel structure in Work section (even with 1 project) for future extensibility
- Keep the same component file structure — no new components needed

## Changes by File

### `index.html`
- Page title: `Swapnil Dahiphale — Staff SRE & AI Engineer`

### `package.json`
- Package name: `swapnil-portfolio`

### `src/components/Landing.tsx`
- First name: `SWAPNIL`
- Last name: `DAHIPHALE`

### `src/components/Navbar.tsx`
- Initials logo: `SD`
- LinkedIn URL: `https://www.linkedin.com/in/swapnil2233/`

### `src/components/About.tsx`
- Bio paragraph:
  > Strategic technologist with 10+ years of experience architecting reliable infrastructure for platforms processing terabytes of daily data. Currently a Staff SRE at VMO India, leading infrastructure for a voice AI agent product and contributing to agentic AI implementations. Creator of OpenSRE.in — an open-source autonomous AI-powered incident investigation platform. Previously engineered highly available infrastructure at MPL (Mobile Premier League), India's largest mobile gaming platform serving 100M+ users. Led cloud migrations and DevOps transformation at Crevise Technologies (acquired by MPL).

### `src/components/WhatIDo.tsx`
Two skill cards:

**Card 1: "Build & Scale"**
- Description: Designing and operating cloud infrastructure at scale — Kubernetes orchestration for 100+ microservices, CI/CD pipelines, observability stacks processing 10+ TB daily log data, Terraform IaC, and high-availability architectures across multiple geographies on AWS and GCP.
- Tags: AWS, Kubernetes, Terraform, Prometheus, Grafana, ELK, Docker, CI/CD, Python

**Card 2: "Agentic AI, Infrastructure & SRE"**
- Description: Building intelligent systems that automate infrastructure operations — multi-agent architectures with LangGraph, autonomous incident investigation with knowledge graphs, RAG pipelines, and AI voice agent infrastructure powering customer support automation.
- Tags: LangGraph, Neo4j, RAG, Python, AI Agents, Voice AI, OpenSRE

### `src/components/Career.tsx`
Five timeline entries (most recent first):

1. **Staff SRE** at VMO India Private Limited — Oct 2023 – Present
   - Strategic execution of Call-AI acquisition, revamping services with containerization and bespoke CI/CD
   - Architected end-to-end dynamic environment provisioning for Health Exchange SaaS platform
   - Leading AI voice agent infrastructure and agentic AI implementations

2. **Staff SRE** at Mobile Premier League (MPL) — Feb 2019 – Sept 2023
   - Led architecture and migration of 100+ microservices to Kubernetes with Istio Mesh
   - Engineered highly available AWS infrastructure for India's largest mobile gaming platform (100M+ users)
   - Implemented log management stack with ELK handling 10+ TB daily data across regions
   - Designed Terraform and Atlantis-based IaC; extensive observability with Prometheus, Thanos, Grafana

3. **Founding Member & DevOps Lead** at Crevise Technologies (Acquired by MPL) — June 2016 – Jan 2019
   - Proposed and implemented highly available, scalable architectures on AWS
   - Implemented CI pipelines with Jenkins, infrastructure automation with Chef
   - Monitoring and logging with DataDog and Loggly

4. **DevOps Engineer** at Whitehedge Technologies — Sept 2015 – June 2016
   - Led cloud migration for Cathay Pacific Airways as project lead and Ansible developer
   - Containerized microservices with Docker and Kubernetes
   - Integrated automated tests with CI pipeline using DroneCI

5. **DevOps Engineer** at Webonise Labs (Haptiq) — Nov 2014 – Aug 2015
   - Managed Linux servers and automated deployment with Webistrano, Capistrano, Chef
   - Deployment automation across ROR, Django, NodeJS, Tomcat stacks
   - LDAP authentication, automated backups, Nagios monitoring

### `src/components/Work.tsx`
Single project (carousel structure preserved):

1. **OpenSRE** — "Agentic AI / SRE" — opensre.in
   - Tools/features: LangGraph, Neo4j, Multi-Agent, Knowledge Graph, 46 Investigation Skills
   - Image: Screenshot of opensre.in (to be captured and saved as `/public/images/opensre.png`)

### `src/components/TechStack.tsx`
Replace 8 tech logos:

| Current | New | Logo Source |
|---------|-----|-------------|
| react2.webp | aws | Copy from OpenSRE repo (`aws.svg`) |
| next2.webp | kubernetes | Copy from OpenSRE repo (`kubernetes.svg`) |
| node2.webp | terraform | Source SVG externally |
| express.webp | python | Source SVG externally |
| mongo.webp | grafana | Copy from OpenSRE repo (`grafana.svg`) |
| mysql.webp | elastic | Copy from OpenSRE repo (`elastic.svg`) |
| typescript.webp | agentic-ai | Find/create icon |
| javascript.webp | langgraph | Source SVG/PNG externally |

Note: Current images are `.webp` format. New logos may be `.svg` — the TechStack component's image loading will need the file references updated accordingly.

### `src/components/Contact.tsx`
- Social links:
  - GitHub: `https://github.com/swapnildahiphale`
  - LinkedIn: `https://www.linkedin.com/in/swapnil2233/`
  - YouTube: `https://www.youtube.com/@Bit-Savvy`
  - Email: `swapnil2233@yahoo.com` (replaces Instagram slot)
- Education: B.E. Computer Science, Pune University (2014) — single entry instead of two
- Footer: "Designed and Developed by Swapnil Dahiphale"

### `src/components/SocialIcons.tsx`
- GitHub: `https://github.com/swapnildahiphale`
- LinkedIn: `https://www.linkedin.com/in/swapnil2233/`
- YouTube: `https://www.youtube.com/@Bit-Savvy`
- Replace Instagram with Email icon/link (`mailto:swapnil2233@yahoo.com`)
- Resume button: Link to `/Swapnil-Dahiphale-Resume-April-2025.pdf`

### Asset Changes
- Remove `/public/Akash_Malhotra.pdf`
- Copy `Swapnil-Dahiphale-Resume-April-2025.pdf` into `/public/`
- Remove old project images no longer referenced (callhq.png, broki.png, orrdr.png, whatsapp.png)
- Add OpenSRE screenshot as `/public/images/opensre.png`
- Copy reusable logos from OpenSRE repo to `/public/images/`
- Source remaining logos (Terraform, Python, LangGraph, Agentic AI)

## Out of Scope
- 3D character model, animations, scroll effects — no changes
- CSS styling — no changes
- Component structure — no changes
- Mobile responsiveness behavior — no changes
