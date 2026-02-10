# Legal Review Criteria (Template)

**This is a template.** Customize it for your project's context, jurisdiction, and risk tolerance.

---

## What to Focus On

The legal review should prioritize:

1. **High-impact risks** — Issues that could result in personal liability, significant financial loss, or legal action
2. **Jurisdiction-specific requirements** — Laws and regulations in the author's and users' locations
3. **Project-specific exposure** — Risks unique to what the project does (financial data, health info, user-generated content, etc.)

---

## Risk Severity Framework

**High Priority (must address before public distribution):**
- Risks that could lead to personal liability or legal claims
- Violations of data protection laws (GDPR, CCPA)
- Missing warranty disclaimers for high-stakes domains (financial, health, safety)
- Trademark infringement

**Medium Priority (address before monetization or scaling):**
- Unclear terms for paid supporters
- Third-party content without license checks
- Security vulnerabilities that could enable data exfiltration
- Missing transparency about data handling

**Low Priority (nice to have):**
- Generic best practices (e.g., CHANGELOG, CONTRIBUTING.md)
- Cosmetic improvements to disclaimers
- Optional documentation (privacy policy, security policy)

---

## Jurisdiction-Specific Considerations

### European Union (GDPR)
- Personal data processing requires legal basis (consent, legitimate interest, contract)
- Users have right to access, erasure, and portability of their data
- Data transfers outside EU require safeguards (Standard Contractual Clauses, adequacy decision)
- Transparency: clear disclosure of what data is collected, why, and where it goes

### United States
- Sectoral privacy laws (CCPA for California, HIPAA for health, COPPA for children)
- No general warranty of fitness unless explicitly promised
- First Amendment protections for speech may apply to content-generation tools
- State-specific requirements vary (some states have data breach notification laws)

### Other Jurisdictions
- [Customize for your location]

---

## Project-Specific Risks

### For Agent-Based Systems
- Prompt injection via third-party content (skills, plugins, documents)
- Execution of user-provided code or commands
- Access to filesystem or sensitive data

### For Financial Tools
- Users making investment decisions based on tool outputs
- Accuracy and timeliness of data
- "Not financial advice" disclaimers required
- Potential regulatory scrutiny (SEC, FCA, etc.)

### For Data Processing Tools
- GDPR/CCPA compliance if handling personal data
- Data security measures (encryption, access controls)
- Data retention and deletion policies

### For Content Generation Tools
- Copyright concerns if training on or outputting copyrighted material
- User agreements about who owns generated content
- DMCA compliance for user-submitted content

---

## Red Flags (Always Investigate)

These patterns should trigger deeper review:

- **No LICENSE file** — always required for open-source distribution
- **Collecting email/name without disclosure** — GDPR violation in EU
- **Trademarked names in project/skill names** — potential trademark claim
- **"Guaranteed updates" or SLA language** — creates legal obligation
- **Reading third-party content without guardrails** — prompt injection risk for agents
- **Financial data + no disclaimer** — high liability exposure
- **No warranty disclaimer** — implied warranty may attach

---

## When to Consult a Lawyer

This skill is a starting point, not legal advice. Consult a lawyer if:

- The project handles regulated data (health, financial, children's data)
- The project is monetized beyond hobby income
- The project operates in multiple jurisdictions with conflicting laws
- The project faces active legal threat or trademark claim
- You're unsure whether you need a legal entity (LLC, corporation)

---

## Customization Instructions

To make this criteria.md useful for your project:

1. **Add your jurisdiction's specific requirements** (replace "European Union" and "United States" sections with what applies to you)
2. **Add project-type-specific risks** (if your project type isn't listed, add it)
3. **Define your risk tolerance** (hobby project vs. business-critical — adjust High/Medium/Low categories accordingly)
4. **List any known red flags** specific to your domain or community
5. **Document what "not legal advice" means in your context** (when to consult a lawyer)

This ensures the review focuses on what actually matters for your project.
