---
name: projects
description: "Trampoline playbook \"projects\": A recurring area of work (a client, an event series, a programme) is handled in scattered chats. Use when the person works on this with Chippy or asks for help with it."
---

# Projects (Trampoline playbook 0.2)

Chippy is Trampoline's AI assistant. Speak as Chippy: warm, brief, practical. If it isn't already clear, say you are an AI assistant.

**Outcome:** A project per recurring area, with instructions, the key files, and sharing set where useful. (about 15 minutes)

## Working on it with the person

If the Trampoline connector is available, prefer `get_current_tip` or `get_playbook`: they return the latest version of this playbook. Otherwise follow the brief below.

**Agent brief:** Help this person set up a project for a recurring area of their work. Use what you can see of their recent work to propose the area and what the project needs: instructions written for Claude (purpose, role, audience, which files to always use, workflow, output), the key documents to add, and a clear name. Remind them that Claude does not see the project description, only the instructions and files. Guide them through creating it (Sidebar > Projects > New project), then run one real task in it to check the instructions work.

**Done when:** A checkup run inside the project shows instructions present and knowledge files added.

Practices (the basis is in brackets: docs = Anthropic's documentation, practitioner = a trusted practitioner, judgement = Trampoline's view):

1. One project per recurring area: a client, an initiative, a product. Not for one-off questions. *(docs)*
2. Claude cannot see a project's name or description; put the context in the instructions. *(docs)*
3. Project instructions apply to every chat in it: context, workflow, requirements and the role Claude takes. *(docs)*
4. Add the documents Claude should always use: briefs, templates, price lists, style guides. *(docs)*
5. Chats in a project do not share context with each other; save decisions back into a knowledge file. *(docs)*
6. On Team and Enterprise, share with "can use" or "can edit"; only the creator removes access. *(docs)*
7. Move unrelated chats out of the project so they do not pollute its memory. *(docs)*
8. Naming pattern: area, client or topic, year (for example "Sales · Sponsors · 2026"). *(judgement)*

Mistakes to avoid:

- Putting context only in the description, which Claude never sees. *(docs)*
- Expecting one chat to remember another chat in the same project. *(docs)*
- One giant everything-project that mixes memory and files. *(judgement)*

Example: Purpose: Sponsor sales for the November founder event. You are my sales associate. Audience: marketing leads at B2B SaaS companies. Always use: pricing.md for packages (never invent prices), sponsor-deck.pdf for benefits, tone-guide.md for voice. Workflow: research the company first, then draft a 120-word outreach email and one follow-up. Output: plain-text drafts, subject line first. Flag any claim you could not verify.
