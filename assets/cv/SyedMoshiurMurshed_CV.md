# Syed Moshiur Murshed

Salzburg, Austria
moshiur.m@gmail.com | LinkedIn: linkedin.com/in/moshiur | GitHub: github.com/moshiur

## Professional Summary

Staff-track Software Engineer with 15+ years of experience building and evolving production-grade systems end-to-end. Spent 14 years owning and continuously improving **Redbex** and **MappRover** — commercial platforms used in civil and energy engineering — across multiple production iterations.

Strong background in C#/.NET, distributed systems, and data-intensive applications, with a focus on maintainable architecture and long-term system evolution. Experienced in combining hands-on development with technical leadership, mentoring engineers, and improving overall engineering quality.

Comfortable working across backend services, APIs, data modeling, DevOps, and cloud-based systems (Azure). Currently delivering client software end-to-end — web platforms, integrations and cloud hosting — with AI-assisted engineering as a standard part of the workflow.

Open to Senior/Lead roles that combine hands-on engineering with team leadership and technical responsibility.

**Key Strength:** Combining hands-on development with team leadership to improve engineering quality, system design, and delivery effectiveness.

## Signature Products

### Redbex — Sensor Data Integration and Analysis Platform

Pöyry's commercial B2B platform for sensor data management across civil and energy engineering — built on OGC Sensor Web Enablement (SWE) standards, deployed as licensed self-hosted installations and as a Pöyry-managed hosted service. Used across civil infrastructure and energy engineering projects handling large time-series sensor datasets.

- Designed and owned the dynamic hierarchical view and filter system — the architectural core of the platform. Views are modelled as composable predicate trees with unlimited depth and dynamic membership evaluation: features join or leave views automatically as data or time changes, with no direct feature-to-view associations. The same mechanism drives reporting, GIS visualisation, analytics, exports, and access control across all deployments
- Designed and built the mapping module — a layered geospatial rendering engine supporting multiple configurable layer types, on-the-fly spatial reference system transformation, and persistable map view templates. Dual-mode: renders interactively in the Redbex UI and exposes a map rendering service producing embeddable images for external systems
- Architected and led a major refactoring of the data import framework — a two-stage pipeline (source extraction → normalised intermediate format → persistence) with a fully configurable generic import type, allowing clients to map any source column to any Redbex field without custom code per deployment
- Built and owned core platform modules — messaging, approval workflows, notifications and alerting, data quality and validation, and reporting and export — before progressively taking ownership of further modules including the charting engine, job execution engine, and CAD export pipeline, ultimately assuming technical ownership of the entire Redbex product
- Led SQL performance engineering: query tuning, index strategy, and data consistency improvements across large time-series sensor observation datasets and hierarchical domain models, significantly improving response times for reporting and GIS queries
- Designed and maintained the open Web API consumed by external clients, MappRover, and third-party integrations — establishing versioning and contract stability as a platform-level concern
- Defined backend architecture patterns adopted across engineering teams, reducing integration friction and establishing a consistent foundation for domain-specific add-on development

### MappRover — Offline-First Geological Mapping Application

iOS application (Xamarin) replacing pen-and-paper geological documentation during tunnel construction — geo-located mapping along a tunnel axis, fully operational without network connectivity, synced to the Redbex platform.

- Designed the offline sync protocol with deterministic conflict handling — a hard requirement given the zero-connectivity environment of active tunnel construction sites, where engineers map geological characteristics directly inside the bore
- Owned the full integration layer between the MappRover iOS client and the Redbex Application Server, including the data synchronisation procedure reconciling offline edits with server-side state modified via the Redbex Smart Client

### GUSS — Construction Industry Cost Estimation Platform

Domain-rich B2B application for the Austrian and German construction industry, specialising in cost estimation and service specification management.

- Worked as lead developer on feature development and platform enhancements across a technically mature product with clear separation of concerns
- Contributed across a complex domain model covering construction cost structures and specification management, gaining depth in Austrian/German construction industry workflows

## Technical Skills

- **Core Engineering:** C#, .NET / ASP.NET Web API, distributed systems, backend services, Entity Framework (EF)
- **Cloud & DevOps:** Azure, AWS (Amplify, Lambda, SQS), Docker, CI/CD, Azure DevOps, Git
- **Data:** SQL (MS SQL Server, PostgreSQL), data modelling, query performance tuning, index strategy
- **Architecture & Patterns:** system design, API design, domain modelling, maintainable architecture
- **Web & Mobile:** Nuxt/Vue, TypeScript, React, Xamarin (iOS/iPad), MVVM
- **Other:** GIS integration, system integration, third-party API integration, privacy/consent engineering (GDPR), technical mentoring

## Professional Experience

### Software Engineer

**Schwarz Works GmbH, Salzburg region, Austria — 07/2026 – present**

End-to-end delivery for a regional software house's clients: requirements with the client, implementation, release, production support and the documentation around it. Two production systems, plus technical direction on further client engagements.

- **Guest self-check-in platform (hospitality client).** Kiosk and wizard guest flows, guest registration (Meldeblatt) and integration with the Austrian tourism registration provider. Diagnosed a production registration failure down to the third-party interface, drove it with the provider, and shipped the corrections across several releases
- **Consent-gated marketing tracking (real-estate client).** Analytics and three advertising tags behind a consent platform on a Nuxt 4 site, six conversion events, environment-scoped IDs so test builds cannot reach live accounts. Built a headless-browser harness to evidence every consent path in two languages; it caught a consent-withdrawal data leak on production that placeholder IDs could not reveal, fixed and verified the same evening
- **Further engagements.** Technical direction for a property-valuation web app (lead capture, branded PDF report, CRM handover, valuation-provider integration) and scoping of a multilingual Google Hotel List feed built from a property-management back end
- Practices: AWS Amplify hosting and CI, release and tagging discipline, evidence-based QA, and AI-assisted engineering (Claude Code, Cursor) as a standard part of the workflow

### Head of Software Development (Technical IC Track)

**AFRY Austria GmbH (former Pöyry Austria GmbH), Salzburg, Austria — 01/2020 – 07/2025**

- Served as principal technical authority for **Redbex** and **MappRover** — owning architecture, backend services, and long-term system evolution across multiple production deployments
- Led and mentored a team of developers, supporting growth in system design, code quality, and engineering practices; conducted code reviews and guided architectural decisions
- Drove platform modernisation by refactoring core subsystems, improving maintainability and scalability without disrupting live client systems
- Partnered closely with product owners and stakeholders to translate complex requirements into reliable, maintainable solutions
- Contributed to hiring and onboarding, helping scale the team and establish consistent engineering standards
- Actively contributed hands-on as a senior developer, working on core backend services, APIs, and system integration
- Worked on cloud-native Azure-based systems (IndustryX, MaterialX), contributing to ASP.NET Web API services and modern DevOps workflows
- Led pilot projects including automation and ML-based processing initiatives, coordinating between teams, clients, and external partners

### Lead Software Engineer

**Pöyry Austria GmbH, Salzburg, Austria — 06/2018 – 01/2020**

- Led design and implementation of major subsystems in Redbex and MappRover, taking ownership from architecture through to production delivery
- Introduced and improved CI/CD pipelines (Azure DevOps), increasing delivery reliability and team consistency
- Mentored developers and promoted adoption of better engineering practices and modern design approaches
- Contributed actively to backend services, APIs, and key system architecture decisions

### Software Engineer

**Pöyry Austria GmbH, Salzburg, Austria — 04/2011 – 06/2018**

- Core contributor to the Redbex platform across the full development lifecycle — analysis, architecture, implementation, and testing
- Designed and built foundational modules: messaging system, approval workflow engine, and GIS-based map components
- Established and maintained CI build infrastructure for stable, repeatable delivery cycles

## Independent Projects (07/2025 – 07/2026)

Six products designed and built end-to-end between employments and since — backend, web, mobile, infrastructure and CI — including a multi-tenant care-operations SaaS, a school management platform with an AI timetable solver, and **Syed.Messaging**, an open-source .NET messaging library (16 NuGet packages, 4,700+ downloads). Roughly 1,160 commits, 460,000 lines of code and 1,190 automated tests, measured from git history. Details: github.com/moshiur

## Earlier Career

**Master Thesis · Carl Zeiss AG, Oberkochen, Germany — 04/2010 – 11/2010**
GPU-Accelerated Lens Polishing Optimisation for Industrial Automation. Designed and implemented OpenCL-based algorithms integrated into C#/.NET industrial systems, reducing computation time by 65% and improving surface quality metrics in production.

**Software Engineer · Adaptive Enterprise Limited, Dhaka, Bangladesh — 03/2006 – 09/2008**
Full-stack .NET engineer on CardAccess legacy migration (Delphi → .NET), building WPF/MVVM facility monitoring, a script server with live code compilation, and an AJAX configuration portal. Cross-continental team with US stakeholders.

**Freelance Programmer · Dhaka, Bangladesh — 04/2004 – 02/2006**
Built multiple web applications for telecoms clients including a document management system, task logger, and registration management platform. Stack: ASP.NET, C#, SQL Server.

## Education

**M.Sc. in Software Technology** — Stuttgart University of Applied Sciences, Stuttgart, Germany — 03/2009 – 11/2010

**B.Sc. in Computer Science** — American International University, Dhaka, Bangladesh — 10/2000 – 08/2006

## Languages

- English: Fluent
- German: Intermediate (B2)
- Bengali: Native
- Hindi: Basic

## References

Available on request.
