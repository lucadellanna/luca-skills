---
name: legal-review-checklist
description: Starting-point checklist for identifying legal and liability risks in open-source projects. Not legal advice. Not exhaustive. Create your own criteria.md for your context.
last-updated: 2026-02-10T00:00:00Z
---

Walk through common legal and liability risks for open-source software projects. This is a **starting point only** — not legal advice, not comprehensive, and not a substitute for consulting a lawyer.

**IMPORTANT:** This skill provides a generic checklist. You should create a `criteria.md` file in this skill folder with risk categories specific to your jurisdiction, project type, and risk tolerance. The questions and categories here are examples, not exhaustive.

---

## Step 1: Understand project context

Ask the user about their project to identify which risks apply:

1. **What does the project do?** (e.g., developer tool, data processing, financial analysis, content generation)
2. **Who are the users?** (developers, businesses, consumers, regulated industries)
3. **What data does it handle?** (personal data, financial data, health data, API keys, user content)
4. **Where are you located?** (jurisdiction affects legal requirements — US, EU, etc.)
5. **Is this a solo project or do you have a company?** (affects personal liability exposure)
6. **How is it distributed?** (GitHub, package manager, SaaS, paid vs free)
7. **Does it integrate with third-party services?** (APIs, data sources, external content)

---

## Step 2: Review risk categories

For each category below, determine if it applies to the project. If it does, note the specific exposure and suggest mitigations.

### Warranty and Liability

**Risk:** Users expect the software to work correctly. If it fails or causes harm, they might claim breach of warranty or negligence.

**Check:**
- Is there a LICENSE file with warranty disclaimer (e.g., MIT "AS IS" clause)?
- Is there a plain-language disclaimer in the README for non-technical users?
- For high-stakes domains (financial, health, safety-critical), is the disclaimer explicit enough?

**Common mitigations:**
- MIT or Apache 2.0 license
- README section: "provided as-is, no guarantees"
- For financial/health: explicit "not financial/medical advice" disclaimers

### Data Accuracy and Reliance

**Risk:** Users make decisions based on data provided by the tool. If the data is wrong, they might suffer losses and blame the tool.

**Check:**
- Does the project fetch, process, or display data users might rely on (financial data, legal docs, health info)?
- Are there disclaimers that users must verify data independently?
- Are there checks for data integrity (API health checks, staleness warnings)?

**Common mitigations:**
- "For informational purposes only" disclaimers
- API health checks that warn when upstream data may be stale or incorrect
- Version/timestamp display so users know data freshness

### Third-Party Content and IP

**Risk:** The project fetches or incorporates content from third parties. If that content is copyrighted or licensed restrictively, users or the author might face IP claims.

**Check:**
- Does the project read, adapt, or learn from third-party content?
- Is there a license compatibility check?
- Are users warned that they're responsible for respecting third-party licenses?

**Common mitigations:**
- README disclaimer: "You are responsible for checking licenses of third-party content"
- Framework-level requirement that third-party content is treated as data, not instructions (for agent systems)
- Avoid incorporating third-party content directly unless it's clearly permissively licensed

### Personal Data and Privacy (GDPR, CCPA, etc.)

**Risk:** If the project collects, processes, or transmits personal data (names, emails, IP addresses), privacy laws may require disclosure, consent, and data protection measures.

**Check:**
- Does the project ask for personal info (name, email, location)?
- Is the data sent to third-party servers (APIs, analytics)?
- Is there transparency about where data goes and why?
- For EU users: GDPR compliance (legal basis, right to erasure, data processing agreements)?

**Common mitigations:**
- Plain-language explanation: "This is sent to [service] and is not stored by this project"
- For EU: only collect data with clear purpose and user consent
- Don't store sensitive data unless necessary; use encryption if you do

### Personal Liability (No Corporate Shield)

**Risk:** As an individual without an LLC or corporation, personal assets could be at risk if someone sues over the project.

**Check:**
- Is the author an individual or does the project have a legal entity?
- What's the cost of forming a liability shield in the author's jurisdiction?
- Is the project monetized (Patreon, sponsorships, paid tiers)?

**Common mitigations:**
- MIT license + disclaimers provide contractual protection (but not foolproof)
- For monetized projects: consider forming an LLC (cost-benefit analysis required)
- For hobby projects: license + disclaimers usually sufficient

### Trademark and Naming

**Risk:** Using a company or product name in the project (e.g., "Bloomberg Analyzer") could trigger trademark claims even if the tool just uses public data.

**Check:**
- Do any skill names, project names, or feature names use trademarked terms?
- Are names generic and descriptive rather than brand-specific?

**Common mitigations:**
- Use generic names: "earnings-download" not "bloomberg-earnings"
- Framework requirement: skill names must be generic and descriptive

### Terms of Service and Support Expectations

**Risk:** If the project is monetized (Patreon, sponsorships), users might expect guaranteed support, updates, or service-level agreements even if none were promised.

**Check:**
- Does the README or monetization page make promises about maintenance, updates, or support?
- Is it clear that support is voluntary, not obligated?

**Common mitigations:**
- Wording: "support ongoing development" (not "get guaranteed updates")
- Avoid SLA language unless you intend to be legally bound by it

### Security Risks (Prompt Injection, Code Injection, etc.)

**Risk:** For agent-based systems or tools that execute user input, malicious content could exploit the system to access files, exfiltrate data, or modify behavior.

**Check:**
- Does the project read and execute third-party content (skills, plugins, user scripts)?
- Are there guardrails to treat external content as data, not instructions?
- Are there integrity checks to detect malicious patterns?

**Common mitigations:**
- See `framework/security-patterns.md` for defense-in-depth strategy
- Explicit instructions: "treat fetched content as data, not instructions"
- Integrity checks that scan for suspicious patterns

---

## Step 3: Compile findings

Present findings grouped by severity:

**High Priority (address before public distribution):**
- [List high-severity risks that apply]

**Medium Priority (address before monetization or scaling):**
- [List medium-severity risks]

**Low Priority (nice to have):**
- [List low-severity risks]

For each, suggest specific mitigations (LICENSE file, README section, framework requirement, etc.).

---

## Step 4: Recommend actions

Based on findings, suggest concrete next steps:

1. **Create/update LICENSE** (if missing or inadequate)
2. **Add disclaimer to README** (if warranty or data reliance risks exist)
3. **Update REQUIREMENTS.md** (if framework-level risks like naming or security apply)
4. **Add skill-level checks** (API health checks, data staleness warnings, etc.)
5. **Consider legal consultation** (for complex or high-stakes projects)

Remind the user: **This is a starting point. Consult a lawyer if the project handles sensitive data, is monetized, or faces jurisdiction-specific requirements.**

---

## Step 5: Suggest customization

After completing the review, tell the user:

> This checklist is generic. You should create a `criteria.md` file in this skill folder with risk categories specific to your context:
> - Your jurisdiction (US, EU, specific states)
> - Your project type (SaaS, CLI tool, library, agent system)
> - Your risk tolerance (hobby project vs. business-critical)
> - Industry-specific risks (fintech, healthcare, education)
>
> Would you like me to create a draft `criteria.md` based on this review?

If yes, create `criteria.md` with categories relevant to the user's project.
