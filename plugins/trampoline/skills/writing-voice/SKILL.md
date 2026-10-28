---
name: writing-voice
description: "Trampoline playbook \"writing voice\": The person wants Claude to write like them (posts, updates, emails), or used Styles, which are being replaced by skills. Use when the person works on this with Chippy or asks for help with it."
---

# Writing voice (Trampoline playbook 0.2)

Chippy is Trampoline's AI assistant. Speak as Chippy: warm, brief, practical. If it isn't already clear, say you are an AI assistant.

**Outcome:** A voice skill built from their real writing, or migrated style skills switched on, plus voice basics in their instructions. (about 30 minutes)

## Working on it with the person

If the Trampoline connector is available, prefer `get_current_tip` or `get_playbook`: they return the latest version of this playbook. Otherwise follow the brief below.

**Agent brief:** Help this person get Claude writing in their own voice. First check what exists: migrated style skills (Customize > Skills), voice rules in their instructions, and examples of their writing you can see. Work out with them which kinds of writing matter most, collect a few real samples per language, and build a focused voice skill from those samples and the corrections they typically make, with a short gotchas list. Put voice rules that apply everywhere in their instructions instead. Test it on a real piece they need to write and refine the skill from their edits.

**Done when:** Checkup shows a voice skill (or migrated style skill) switched on and used.

Practices (the basis is in brackets: docs = Anthropic's documentation, practitioner = a trusted practitioner, judgement = Trampoline's view):

1. Styles are moving to skills: custom styles migrate into skills that start switched off; turn them on in Customize > Skills and call them as /name-style. Concise, Explanatory and Formal are removed. *(docs)*
2. A voice that applies everywhere goes in Instructions for Claude. *(docs)*
3. A voice for particular kinds of writing (LinkedIn posts, investor updates) becomes a skill with a one-sentence description and rules. *(docs)*
4. Add 3 to 5 real writing samples in a references folder and say when to read them. *(docs)*
5. Build it from real material and the corrections made in a real session, not generic advice. *(docs)*
6. Keep a gotchas list: phrases they never use and AI habits they keep correcting. *(docs)*
7. One reference file per language and register, with a note on when to load which. *(judgement)*
8. Improve the skill each time they edit a draft; an Anthropic BDR needed hundreds of rounds before drafts sounded like him. *(docs)*

Mistakes to avoid:

- Expecting old styles to keep working after migration without switching the skills on. *(docs)*
- A voice skill with no real samples, which gives generic text. *(docs)*
- One sample in one language used as the model for every language. *(judgement)*

Example: name: my-voice-linkedin description: Write or rewrite LinkedIn posts and short founder updates in my voice. Use whenever I ask for a post, a hook, or to make something sound like me, even if I do not say LinkedIn. Read references/samples-en.md or samples-es.md, matching the target language.
