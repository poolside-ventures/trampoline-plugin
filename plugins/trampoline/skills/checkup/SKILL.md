---
name: checkup
description: "Chippy's setup checkup for Trampoline. Use when the person says \"Chippy, check my setup\", asks for a Trampoline or Chippy checkup, or a scheduled task runs it. Claude inspects its own setup (instructions, memory, connectors, skills, project, recent activity) and scores how the person's recent prompts follow best practice, reports it as counts, scores and yes/no answers, never content, and sends it to the Trampoline connector for a scorecard and tips."
---

# Chippy checkup (v0.11)

You are running a setup checkup for Chippy, Trampoline's AI assistant. The goal is to learn what you can detect about this person's Claude setup and use **from inside this conversation, without asking them anything**. Report only facts: yes/no answers, counts, dates, names of tools or skills, and short generic task labels. Never quote or summarise the content of their instructions, memory, files or chats, and never include names of people, clients or companies.

Do not ask the person questions, and work quietly: don't call tools that show cards or suggestions to the person, such as connector suggestions, a list of their skills or "try it" prompts. Count from what is in your context and from tool-search results instead. If you cannot see something, say "cannot see" rather than guessing. Be honest about uncertainty: mark each answer as **seen** (you can directly observe it in your context or a tool result), **inferred** (indirect evidence) or **cannot see**.

## Steps

1. **Surface.** Which surface are you running in, as far as you can tell: claude.ai chat, a claude.ai project, Cowork, a Cowork scheduled task, Claude Code, Claude in Chrome, Claude for Microsoft 365, Slack, other.
2. **Context.** Are there account-level instructions from the person ("Instructions for Claude" or user preferences) in your context? Rough length: none, short (under 50 words), medium, long (over 300 words). Say where you found them: a separate instructions block, or inside memory. Is a writing style applied?
3. **Memory.**
   - Is any memory about this person present in your context, or do you have memory tools?
   - If you have memory tools, use them read-only to count topics or entries. Do not show their content.
   - Count the memory items or topics. Note the most recent date you can see on any memory item, and count how many items were updated in the last 7 and 30 days, if dates are visible.
4. **Project.** Are you inside a project? If yes: are project instructions present (yes/no, rough length), how many project knowledge files can you see, and is there project-scoped memory?
5. **Connectors.** List the names of the connectors or integrations you can call (for example Google Drive, Gmail, Google Calendar, Slack, Notion, Microsoft 365). Exclude built-in tools and the Trampoline connector itself.
   - **Before you report none, look for tools that load on demand.** If you have a tool-search tool, or a registry or list of deferred or not-loaded tools, search it (for example for "gmail", "drive", "calendar", "slack", "notion", "microsoft") and count connectors found there.
   - Report the connectors in four lists:
     - loaded;
     - available on demand;
     - installed but not connected;
     - needing reconnection.
   - Do not call any connector's own tools.
6. **Built-in features.** Which of these do you have right now: web search, web fetch, code execution or file creation, artifacts, past-chat search, research mode, browser control, scheduled tasks.
7. **Skills.** Count the skills available to you. Split them into Anthropic built-in skills (names starting with an Anthropic prefix, or clearly generic file-format skills) and others (company or personal). List the names of the others.
8. **Recent activity.**
   - If you have a past-chat tool (for example recent chats or conversation search), call it read-only to look at recent conversations.
   - **Cover the full last 30 days.** Recent-chat tools return a limited number of chats per call (often 20). Call again with an earlier "before" date (the oldest chat you have so far) until you reach chats older than 30 days or there are no more. Report how many calls you made and whether you reached the 30-day mark.
   - Report: the number of chats you can see from the last 7 days and the last 30 days, the number of distinct days with activity, and the date of the oldest chat you can see.
   - **Task mix:** count chats by kind, using only these labels: writing, communication (email, messages), analysis, research, planning, coding, learning, other.
   - **Repeated tasks:** list kinds of task that appear in 3 or more chats in the last 30 days.
     - For each, give a short generic label of 2 to 4 words (for example "investor update", "meeting prep", "market research"), its kind from the labels above, and the count.
     - Labels must be generic: no names of people, clients, companies or products.
   - **Features used:** count chats where you can see that a feature was used (research mode, documents or artifacts, file analysis or code, web search). If the chat summaries don't show this, write "cannot see" instead of 0.
   - **Connectors used:** list the connectors you can see were used in recent chats, or "cannot see".
   - Do not quote titles or content.
   - If no past-chat tool exists, say whether it looks switched off in settings or not offered on this surface, and why you think so.
9. **Connector value.** For each repeated task, judge whether a connector would clearly help with it. Ignore the connection state: a connector can be loaded, on demand, not connected, needing reconnection, or not installed at all.
   - Base the judgement only on each connector's own description and tool names, as shown in your tool list or in connector registry results.
   - If you have a connector registry search, you may search it with two or three generic keywords per repeated task to find connectors that aren't installed.
   - **Grade the fit:**
     - **strong:** the task needs data or an action in that service, and the description or tool names show the connector provides it (for example trademark searches for naming work).
     - **possible:** the connector could help with part of the task.
     - **weak:** only the topic overlaps (for example a calendar connector for planning event formats). List weak matches only if there is nothing better, and never more than one.
   - Give the reason in 15 words or fewer, taken from the description or tool names.
   - Do not call any connector's own tools.
10. **Prompt practices.** How the person asks, scored against Trampoline's best practices. Only scores are sent, never the prompts.
   - If past-chat search is switched off or not offered, skip this step and set `reason_if_none` to `past_chat_search_off`. That is a setup gap: the scorecard will say so.
   - Call the Trampoline connector's `get_prompt_practices` tool for the current practices, scale and how to assess. If the connector is not available, skip this step (`reason_if_none`: `other`).
   - With the past-chat tool, look at chats from the last 7 days. Pick up to 10 of the person's own messages that ask Claude to do something, from different chats where you can: opening requests, and follow-ups that react to an answer. Skip greetings, one-word replies, bare slash commands (for example `/chippy-checkup`), chats about Chippy or Trampoline themselves, and text Claude drafted for them.
   - If the results show only summaries or titles and not the person's own words, don't guess: set `reason_if_none` to `only_summaries_visible`.
   - Score each message on every practice: 0, 1, 2, or null when it does not apply, using the level descriptions. Reason briefly before each score. A short prompt can score 2; length is not quality.
   - In the report, give each scored message its date and task kind (same labels as the task mix) and the scores. Nothing else: no text, titles or topics.
11. **Limits.** List what you could not determine and why (for example "cannot see projects other than the current one").

## The report

Build exactly one JSON object. It is only for the `submit_checkup` tool: never show it, or any code or field names, to the person.

```json
{
  "chippy_checkup_version": "0.11",
  "date": "YYYY-MM-DD",
  "surface": {"value": "", "confidence": "seen|inferred|cannot see"},
  "context": {"instructions_present": null, "instructions_length": "none|short|medium|long", "instructions_location": "separate|in_memory|cannot see", "style_applied": null, "confidence": ""},
  "memory": {"present": null, "memory_tools": null, "item_count": null, "latest_item_date": null, "updated_last_7_days": null, "updated_last_30_days": null, "confidence": ""},
  "project": {"in_project": null, "instructions_present": null, "knowledge_file_count": null, "project_memory": null, "confidence": ""},
  "connectors": {"loaded": [], "on_demand": [], "not_connected": [], "needs_reconnect": [], "used_recently": "cannot see or a list", "tool_search_available": null,
    "value_matches": [{"connector": "", "state": "loaded|on_demand|not_connected|needs_reconnect|not_installed", "task": "", "fit": "strong|possible|weak", "why": ""}], "confidence": ""},
  "features": {"web_search": null, "web_fetch": null, "code_or_files": null, "artifacts": null, "past_chat_search": null, "research": null, "browser": null, "scheduled_tasks": null},
  "skills": {"count": null, "builtin_count": null, "custom_names": [], "confidence": ""},
  "activity": {
    "chats_last_7_days": null, "chats_last_30_days": null, "active_days_last_30": null, "oldest_chat_seen": null,
    "reached_30_days": null, "calls_made": null,
    "task_mix": {},
    "repeated_tasks": [{"label": "", "kind": "", "count": 0}],
    "features_used": {"research": null, "artifacts": null, "code_or_files": null, "web_search": null},
    "past_chat_reason_if_missing": "", "confidence": ""
  },
  "prompts": {"chats_looked_at": null, "assessed": null, "reason_if_none": null,
    "items": [{"date": "YYYY-MM-DD", "kind": "writing", "scores": {"clear_task": 2, "context_and_purpose": 1, "output_and_constraints": null}}]},
  "cannot_determine": []
}
```

## Sending it

The people using Chippy don't work with code. Speak plainly and keep it short: no JSON, no field names, no technical terms.

1. Check the report once more for anything that is not a count, score, date, yes/no, tool or skill name or generic label. Remove names of people, clients, companies or products, and quotes.
2. In two or three plain sentences, say what you are sending, for example: "I've looked at your setup. I'm sending Trampoline only counts and yes/no answers, like that memory is on with 28 items, 3 apps aren't connected yet, and you used Claude on 19 days this month. Never your chats or files."
3. Then call the Trampoline connector's `submit_checkup` tool with the report straight away; don't ask for permission first (connecting Trampoline was the permission). Use `trigger: "scheduled"` when this runs as a scheduled task, otherwise `"on_demand"`. If the person asks you not to send it, don't.
4. Chippy's card shows the scorecard and tips. In a few plain lines, point out the most useful gap or tip and offer to work on it now (then follow the `work-on-tip` skill). If prompt practices were scored, name the practice with the most room to grow in one sentence, with what good looks like.
5. If the Trampoline connector is not available, say so and point the person to https://trampoline.tech/setup. Do not send the report anywhere else.

