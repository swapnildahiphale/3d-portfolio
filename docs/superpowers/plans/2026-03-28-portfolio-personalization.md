# Portfolio Personalization Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Replace all personal content in the 3D portfolio from Akash Malhotra to Swapnil Dahiphale — no visual or structural changes.

**Architecture:** Pure content swap across ~10 component files + asset replacement. Each task modifies one file (or a small group of related files). No new components, no CSS changes, no animation changes.

**Tech Stack:** React 18, TypeScript, Vite, Three.js (existing — unchanged)

---

### Task 1: Assets — Copy Logos and Resume

**Files:**
- Copy logos from: `/Users/Swapnil/workspace/swapnil/OpenSRE/website/launch/site/public/logos/` (aws.svg, kubernetes.svg, grafana.svg, elastic.svg)
- Copy to: `public/images/` (as aws.webp, kubernetes.webp, grafana.webp, elastic.webp — or keep .svg and update refs)
- Copy resume: `Swapnil-Dahiphale-Resume-April-2025.pdf` → `public/Swapnil-Dahiphale-Resume-April-2025.pdf`
- Source externally: terraform.svg, python.svg, langgraph.png, agentic-ai.svg

**Note on image format:** The TechStack component uses `THREE.TextureLoader()` which supports PNG, JPG, and WebP but **not SVG**. SVG logos must be converted to PNG or WebP before use.

- [ ] **Step 1: Copy reusable logos from OpenSRE repo**

```bash
cp /Users/Swapnil/workspace/swapnil/OpenSRE/website/launch/site/public/logos/aws.svg public/images/aws.svg
cp /Users/Swapnil/workspace/swapnil/OpenSRE/website/launch/site/public/logos/kubernetes.svg public/images/kubernetes.svg
cp /Users/Swapnil/workspace/swapnil/OpenSRE/website/launch/site/public/logos/grafana.svg public/images/grafana.svg
cp /Users/Swapnil/workspace/swapnil/OpenSRE/website/launch/site/public/logos/elastic.svg public/images/elastic.svg
```

- [ ] **Step 2: Convert SVG logos to PNG for Three.js TextureLoader compatibility**

Use `sips` (macOS built-in) or a similar tool to convert each SVG to PNG:

```bash
# If sips doesn't handle SVG, use qlmanage or a node script:
# Option A: Use qlmanage (macOS)
qlmanage -t -s 512 -o public/images/ public/images/aws.svg
# Then rename the output files

# Option B: Install and use sharp via a quick node script
node -e "
const sharp = require('sharp');
const logos = ['aws', 'kubernetes', 'grafana', 'elastic'];
logos.forEach(name => {
  sharp('public/images/' + name + '.svg')
    .resize(512, 512, { fit: 'contain', background: { r: 0, g: 0, b: 0, alpha: 0 } })
    .png()
    .toFile('public/images/' + name + '.png');
});
"
```

If neither approach works easily, manually download PNG versions of these logos from the web. The key requirement is that each logo ends up as a raster image (PNG or WebP) at `public/images/<name>.png`.

- [ ] **Step 3: Source remaining logos (Terraform, Python, LangGraph, Agentic AI)**

Download PNG logos and save to `public/images/`:
- `public/images/terraform.png` — Terraform logo
- `public/images/python.png` — Python logo
- `public/images/langgraph.png` — LangGraph logo (LangChain ecosystem logo or text-based)
- `public/images/agentic-ai.png` — A suitable AI/agent icon (brain + circuit, robot icon, or similar)

These can be fetched from the web or created. Each should be roughly 512×512px with transparent background.

- [ ] **Step 4: Copy resume PDF to public directory**

```bash
cp Swapnil-Dahiphale-Resume-April-2025.pdf public/Swapnil-Dahiphale-Resume-April-2025.pdf
```

- [ ] **Step 5: Capture OpenSRE screenshot**

Take a screenshot of https://www.opensre.in and save as `public/images/opensre.png`. Use browser tools or a CLI screenshot utility. Aim for ~1200×800px.

- [ ] **Step 6: Remove old assets no longer needed**

```bash
rm public/Akash_Malhotra.pdf
rm public/images/callhq.png
rm public/images/broki.png
rm public/images/orrdr.png
rm public/images/whatsapp.png
```

- [ ] **Step 7: Commit**

```bash
git add public/images/aws.png public/images/kubernetes.png public/images/grafana.png public/images/elastic.png \
       public/images/terraform.png public/images/python.png public/images/langgraph.png public/images/agentic-ai.png \
       public/images/opensre.png public/Swapnil-Dahiphale-Resume-April-2025.pdf
git add -u  # stages deletions
git commit -m "chore: swap assets — add Swapnil's logos, resume, and project screenshot; remove Akash's assets"
```

---

### Task 2: Update index.html and package.json

**Files:**
- Modify: `index.html:8`
- Modify: `package.json:2`

- [ ] **Step 1: Update page title in index.html**

Change line 8 from:
```html
  <title>Akash Malhotra — Co-Founder & Developer</title>
```
to:
```html
  <title>Swapnil Dahiphale — Staff SRE & AI Engineer</title>
```

- [ ] **Step 2: Update package name in package.json**

Change line 2 from:
```json
  "name": "akash-portfolio",
```
to:
```json
  "name": "swapnil-portfolio",
```

- [ ] **Step 3: Verify build still works**

```bash
npm run build
```

Expected: Clean build with no errors.

- [ ] **Step 4: Commit**

```bash
git add index.html package.json
git commit -m "chore: update page title and package name to Swapnil Dahiphale"
```

---

### Task 3: Update Landing.tsx

**Files:**
- Modify: `src/components/Landing.tsx:10-26`

- [ ] **Step 1: Replace name and title**

Replace lines 10–26 with:
```tsx
            <h2>Hello! I'm</h2>
            <h1>
              SWAPNIL
              <br />
              <span>DAHIPHALE</span>
            </h1>
          </div>
          <div className="landing-info">
            <h3>Staff SRE &</h3>
            <h2 className="landing-info-h2">
              <div className="landing-h2-1">AI</div>
              <div className="landing-h2-2">Platform</div>
            </h2>
            <h2>
              <div className="landing-h2-info">Platform</div>
              <div className="landing-h2-info-1">AI</div>
            </h2>
```

The animated text flip currently alternates between "Tech" and "Business". The new version alternates between "AI" and "Platform" to reflect Swapnil's dual focus on AI engineering and platform/infrastructure.

- [ ] **Step 2: Verify in dev server**

```bash
npm run dev
```

Open http://localhost:5173 — confirm "SWAPNIL DAHIPHALE" appears with "Staff SRE & AI/Platform" subtitle.

- [ ] **Step 3: Commit**

```bash
git add src/components/Landing.tsx
git commit -m "feat: update Landing with Swapnil's name and title"
```

---

### Task 4: Update Navbar.tsx

**Files:**
- Modify: `src/components/Navbar.tsx:46,49,55`

- [ ] **Step 1: Replace initials and LinkedIn URL**

Change the initials on line 46 from `AM` to `SD`:
```tsx
          SD
```

Change the LinkedIn href on line 49 from:
```tsx
          href="https://www.linkedin.com/in/akashrmalhotra/"
```
to:
```tsx
          href="https://www.linkedin.com/in/swapnil2233/"
```

Change the LinkedIn display text on line 55 from:
```tsx
          linkedin.com/in/akashrmalhotra
```
to:
```tsx
          linkedin.com/in/swapnil2233
```

- [ ] **Step 2: Commit**

```bash
git add src/components/Navbar.tsx
git commit -m "feat: update Navbar with Swapnil's initials and LinkedIn"
```

---

### Task 5: Update About.tsx

**Files:**
- Modify: `src/components/About.tsx:8-13`

- [ ] **Step 1: Replace bio paragraph**

Replace the entire `<p>` content (lines 8–13) with:
```tsx
        <p className="para">
          Strategic technologist with 10+ years of experience architecting
          reliable infrastructure for platforms processing terabytes of daily
          data. Currently a Staff SRE at VMO India, leading infrastructure for a
          voice AI agent product and contributing to agentic AI implementations.
          Creator of OpenSRE.in — an open-source autonomous AI-powered incident
          investigation platform. Previously engineered highly available
          infrastructure at MPL (Mobile Premier League), India's largest mobile
          gaming platform serving 100M+ users. Led cloud migrations and DevOps
          transformation at Crevise Technologies (acquired by MPL).
        </p>
```

- [ ] **Step 2: Commit**

```bash
git add src/components/About.tsx
git commit -m "feat: update About section with Swapnil's bio"
```

---

### Task 6: Update WhatIDo.tsx

**Files:**
- Modify: `src/components/WhatIDo.tsx:89-104` (Card 1)
- Modify: `src/components/WhatIDo.tsx:127-143` (Card 2)

- [ ] **Step 1: Replace Card 1 content (currently "AI & AUTOMATION")**

Replace lines 89–104 (the `what-content-in` div for Card 1) with:
```tsx
            <div className="what-content-in">
              <h3>BUILD &amp; SCALE</h3>
              <h4>Cloud Infrastructure at Scale</h4>
              <p>
                Designing and operating cloud infrastructure at scale —
                Kubernetes orchestration for 100+ microservices, CI/CD pipelines,
                observability stacks processing 10+ TB daily log data, Terraform
                IaC, and high-availability architectures across multiple
                geographies on AWS and GCP.
              </p>
              <h5>Skillset & tools</h5>
              <div className="what-content-flex">
                <div className="what-tags">AWS</div>
                <div className="what-tags">Kubernetes</div>
                <div className="what-tags">Terraform</div>
                <div className="what-tags">Prometheus</div>
                <div className="what-tags">Grafana</div>
                <div className="what-tags">ELK</div>
                <div className="what-tags">Docker</div>
                <div className="what-tags">CI/CD</div>
                <div className="what-tags">Python</div>
              </div>
              <div className="what-arrow"></div>
            </div>
```

- [ ] **Step 2: Replace Card 2 content (currently "BUILD & SCALE")**

Replace lines 126–144 (the `what-content-in` div for Card 2) with:
```tsx
            <div className="what-content-in">
              <h3>AGENTIC AI, INFRASTRUCTURE &amp; SRE</h3>
              <h4>Intelligent Infrastructure Automation</h4>
              <p>
                Building intelligent systems that automate infrastructure
                operations — multi-agent architectures with LangGraph, autonomous
                incident investigation with knowledge graphs, RAG pipelines, and
                AI voice agent infrastructure powering customer support
                automation.
              </p>
              <h5>Skillset & tools</h5>
              <div className="what-content-flex">
                <div className="what-tags">LangGraph</div>
                <div className="what-tags">Neo4j</div>
                <div className="what-tags">RAG</div>
                <div className="what-tags">Python</div>
                <div className="what-tags">AI Agents</div>
                <div className="what-tags">Voice AI</div>
                <div className="what-tags">OpenSRE</div>
              </div>
              <div className="what-arrow"></div>
            </div>
```

- [ ] **Step 3: Commit**

```bash
git add src/components/WhatIDo.tsx
git commit -m "feat: update WhatIDo with Build & Scale and Agentic AI cards"
```

---

### Task 7: Update Career.tsx

**Files:**
- Modify: `src/components/Career.tsx:15-71` (replace all 4 career entries with 5 new ones)

- [ ] **Step 1: Replace all career entries**

Replace the entire `career-info` div content (lines 11–71, from `<div className="career-info">` through its closing `</div>`) with:
```tsx
        <div className="career-info">
          <div className="career-timeline">
            <div className="career-dot"></div>
          </div>
          <div className="career-info-box">
            <div className="career-info-in">
              <div className="career-role">
                <h4>Staff SRE</h4>
                <h5>VMO India Private Limited</h5>
              </div>
              <h3>NOW</h3>
            </div>
            <p>
              Strategic execution of Call-AI acquisition, revamping services with
              containerization and bespoke CI/CD. Architected end-to-end dynamic
              environment provisioning for Health Exchange SaaS platform. Leading
              AI voice agent infrastructure and agentic AI implementations.
            </p>
          </div>
          <div className="career-info-box">
            <div className="career-info-in">
              <div className="career-role">
                <h4>Staff SRE</h4>
                <h5>Mobile Premier League (MPL)</h5>
              </div>
              <h3>2019–23</h3>
            </div>
            <p>
              Led architecture and migration of 100+ microservices to Kubernetes
              with Istio Mesh. Engineered highly available AWS infrastructure for
              India's largest mobile gaming platform (100M+ users). Implemented
              log management with ELK handling 10+ TB daily data. Designed
              Terraform and Atlantis-based IaC; observability with Prometheus,
              Thanos, and Grafana.
            </p>
          </div>
          <div className="career-info-box">
            <div className="career-info-in">
              <div className="career-role">
                <h4>Founding Member &amp; DevOps Lead</h4>
                <h5>Crevise Technologies (Acquired by MPL)</h5>
              </div>
              <h3>2016–19</h3>
            </div>
            <p>
              Proposed and implemented highly available, scalable architectures
              on AWS. CI pipelines with Jenkins, infrastructure automation with
              Chef. Monitoring and logging with DataDog and Loggly.
            </p>
          </div>
          <div className="career-info-box">
            <div className="career-info-in">
              <div className="career-role">
                <h4>DevOps Engineer</h4>
                <h5>Whitehedge Technologies</h5>
              </div>
              <h3>2015–16</h3>
            </div>
            <p>
              Led cloud migration for Cathay Pacific Airways as project lead and
              Ansible developer. Containerized microservices with Docker and
              Kubernetes. Integrated automated tests with CI pipeline using
              DroneCI.
            </p>
          </div>
          <div className="career-info-box">
            <div className="career-info-in">
              <div className="career-role">
                <h4>DevOps Engineer</h4>
                <h5>Webonise Labs (Haptiq)</h5>
              </div>
              <h3>2014–15</h3>
            </div>
            <p>
              Managed Linux servers and automated deployment with Webistrano,
              Capistrano, and Chef. Deployment automation across ROR, Django,
              NodeJS, and Tomcat stacks. LDAP authentication, automated backups,
              and Nagios monitoring.
            </p>
          </div>
        </div>
```

- [ ] **Step 2: Commit**

```bash
git add src/components/Career.tsx
git commit -m "feat: update Career with Swapnil's 5 work experience entries"
```

---

### Task 8: Update Work.tsx

**Files:**
- Modify: `src/components/Work.tsx:6-35` (replace projects array)

- [ ] **Step 1: Replace the projects array**

Replace the entire `projects` array (lines 6–35) with:
```tsx
const projects = [
  {
    title: "OpenSRE",
    category: "Agentic AI / SRE",
    tools: "LangGraph, Neo4j, Multi-Agent, Knowledge Graph, 46 Investigation Skills",
    image: "/images/opensre.png",
    link: "https://opensre.in",
  },
];
```

- [ ] **Step 2: Commit**

```bash
git add src/components/Work.tsx
git commit -m "feat: update Work section with OpenSRE project"
```

---

### Task 9: Update TechStack.tsx

**Files:**
- Modify: `src/components/TechStack.tsx:15-24` (replace imageUrls array)

- [ ] **Step 1: Replace the imageUrls array**

Replace lines 15–24 with:
```tsx
const imageUrls = [
  "/images/aws.png",
  "/images/kubernetes.png",
  "/images/terraform.png",
  "/images/python.png",
  "/images/grafana.png",
  "/images/elastic.png",
  "/images/agentic-ai.png",
  "/images/langgraph.png",
];
```

Ensure the file extensions match whatever format the logos were saved in during Task 1.

- [ ] **Step 2: Commit**

```bash
git add src/components/TechStack.tsx
git commit -m "feat: update TechStack with Swapnil's technology logos"
```

---

### Task 10: Update Contact.tsx

**Files:**
- Modify: `src/components/Contact.tsx:12-68` (social links, education, footer)

- [ ] **Step 1: Replace entire contact content**

Replace the `contact-flex` div content (lines 9–77) with:
```tsx
        <div className="contact-flex">
          <div className="contact-box">
            <h4>Connect</h4>
            <p>
              <a
                href="https://www.linkedin.com/in/swapnil2233/"
                target="_blank"
                rel="noreferrer"
                data-cursor="disable"
              >
                LinkedIn — swapnil2233
              </a>
            </p>
            <h4>Education</h4>
            <p>
              B.E. Computer Science, Pune University — 2014
            </p>
          </div>
          <div className="contact-box">
            <h4>Social</h4>
            <a
              href="https://github.com/swapnildahiphale"
              target="_blank"
              rel="noreferrer"
              data-cursor="disable"
              className="contact-social"
            >
              GitHub <MdArrowOutward />
            </a>
            <a
              href="https://www.linkedin.com/in/swapnil2233/"
              target="_blank"
              rel="noreferrer"
              data-cursor="disable"
              className="contact-social"
            >
              LinkedIn <MdArrowOutward />
            </a>
            <a
              href="https://www.youtube.com/@Bit-Savvy"
              target="_blank"
              rel="noreferrer"
              data-cursor="disable"
              className="contact-social"
            >
              YouTube <MdArrowOutward />
            </a>
            <a
              href="mailto:swapnil2233@yahoo.com"
              data-cursor="disable"
              className="contact-social"
            >
              Email <MdArrowOutward />
            </a>
          </div>
          <div className="contact-box">
            <h2>
              Designed and Developed <br /> by <span>Swapnil Dahiphale</span>
            </h2>
            <h5>
              <MdCopyright /> 2026
            </h5>
          </div>
        </div>
```

- [ ] **Step 2: Commit**

```bash
git add src/components/Contact.tsx
git commit -m "feat: update Contact with Swapnil's links, education, and footer"
```

---

### Task 11: Update SocialIcons.tsx

**Files:**
- Modify: `src/components/SocialIcons.tsx:1-6` (imports — replace FaInstagram with MdEmail or similar)
- Modify: `src/components/SocialIcons.tsx:62-98` (social links)
- Modify: `src/components/SocialIcons.tsx:101` (resume path)

- [ ] **Step 1: Update imports — replace Instagram with Email icon**

Replace line 3–4:
```tsx
  FaInstagram,
  FaLinkedinIn,
```
with:
```tsx
  FaLinkedinIn,
```

Add an email icon import. `react-icons` has `MdEmail` from Material Design:
```tsx
import { MdEmail } from "react-icons/md";
```

Full import block becomes:
```tsx
import {
  FaGithub,
  FaLinkedinIn,
  FaYoutube,
} from "react-icons/fa6";
import { MdEmail } from "react-icons/md";
import "./styles/SocialIcons.css";
import { TbNotes } from "react-icons/tb";
import { useEffect } from "react";
import HoverLinks from "./HoverLinks";
```

- [ ] **Step 2: Replace social link URLs and icons**

Replace the 4 social `<span>` blocks (lines 62–98) with:
```tsx
        <span>
          <a
            href="https://github.com/swapnildahiphale"
            target="_blank"
            rel="noreferrer"
          >
            <FaGithub />
          </a>
        </span>
        <span>
          <a
            href="https://www.linkedin.com/in/swapnil2233/"
            target="_blank"
            rel="noreferrer"
          >
            <FaLinkedinIn />
          </a>
        </span>
        <span>
          <a
            href="https://www.youtube.com/@Bit-Savvy"
            target="_blank"
            rel="noreferrer"
          >
            <FaYoutube />
          </a>
        </span>
        <span>
          <a
            href="mailto:swapnil2233@yahoo.com"
          >
            <MdEmail />
          </a>
        </span>
```

- [ ] **Step 3: Update resume link**

Change line 101 from:
```tsx
        href="/Akash_Malhotra.pdf"
```
to:
```tsx
        href="/Swapnil-Dahiphale-Resume-April-2025.pdf"
```

- [ ] **Step 4: Commit**

```bash
git add src/components/SocialIcons.tsx
git commit -m "feat: update SocialIcons with Swapnil's links and email icon"
```

---

### Task 12: Final Verification

**Files:** None — verification only

- [ ] **Step 1: Run build to catch any TypeScript or compilation errors**

```bash
npm run build
```

Expected: Clean build with no errors.

- [ ] **Step 2: Run lint**

```bash
npm run lint
```

Expected: No new lint errors introduced.

- [ ] **Step 3: Visual verification in dev server**

```bash
npm run dev
```

Open http://localhost:5173 and check each section:
- Landing: "SWAPNIL DAHIPHALE" with "Staff SRE & AI/Platform"
- Navbar: "SD" initials, LinkedIn link to swapnil2233
- About: New bio paragraph
- What I Do: "BUILD & SCALE" and "AGENTIC AI, INFRASTRUCTURE & SRE" cards
- Career: 5 entries from VMO India through Webonise Labs
- Work: Single OpenSRE project with screenshot
- Tech Stack: 8 new tech logos floating as 3D spheres
- Contact: GitHub, LinkedIn, YouTube, Email links + Pune University education
- Social sidebar: 4 icons (GitHub, LinkedIn, YouTube, Email) + Resume button
- Resume button: Opens Swapnil's resume PDF

- [ ] **Step 4: Commit any fixes if needed, then final commit**

```bash
git add -A
git commit -m "chore: final verification and cleanup for Swapnil's portfolio"
```
