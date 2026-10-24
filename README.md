# Trampoline plugin for Claude

Chippy, Trampoline's AI assistant, checks how your Claude is set up, finds the real gaps, and helps you fix them in your own
Claude. It sends Trampoline only yes or no answers, counts, dates, tool and skill names and short generic labels, never your
chats, files or the names of people, clients or companies, and you see every report before it is sent.

## Add it to Claude

1. Sign up at [trampoline.tech](https://trampoline.tech).
2. In Claude: **Customize > Plugins > Add > Add marketplace**, enter `poolside-ventures/trampoline-plugin`, and install
   **Trampoline**.
3. In the plugin's **Connectors** tab, connect **Trampoline** and sign in.
4. Say "Chippy, check my setup".

Plugins need a paid Claude plan (Pro, Max, Team or Enterprise).

## What's inside

- `checkup`: Chippy's setup checkup.
- `show-tips`: "Chippy, show me my latest tips".
- `work-on-tip`: works through your active tip with you.
- One skill per Trampoline playbook (instructions, memory, projects, research, skills, writing voice, scheduled tasks).
- The Trampoline connector (`https://trampoline.tech/mcp`).

This repository is published from Trampoline's private repository; changes made here are overwritten.
[Privacy policy](https://trampoline.tech/privacy) · [Terms](https://trampoline.tech/terms)
