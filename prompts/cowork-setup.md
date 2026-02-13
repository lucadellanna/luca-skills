# Getting Claude to Improve Over Time (Simple Setup)

## 1) Install & basic privacy
- Install **Claude Desktop**: https://claude.com/download
- Open **Settings → Privacy** and deselect **"Help improve Claude"** so your conversations and preferences remain private.

## 2) Start a chat
- Open Claude Desktop
- **If you have a paid plan:** Click **"Cowork"** at the top, then start a new chat. You'll see a prompt to select a folder — I suggest creating a "Claude" folder in your top-level folder (for example, `Users/Luca/Claude`).
- **If you're on the free plan:** Start a regular chat. Then **(very important)** paste the following and send the message: 
  - Add this to your memory: Every time you create or edit a skill, you must use the present_file tool to show me the finished skill, and clearly tell me to click "Copy to your skills" to save it. Warn me that the skill will be lost if I don't click that button.

## 3) Create the "reflect" skill
A **skill** is a saved instruction that Claude remembers across all your future chats. It's the basic building block to ensure that Claude gets better as you keep using it.

Paste this and send it:

---

Create a skill called "reflect".
When I type "reflect", you should spin a subagent to:
1. Review what we've done in this chat.
2. Identify mistakes, friction, or unclear outputs.
3. Propose a short list of concrete improvements.
4. Ask me which of these you should remember for future chats.

If any skills were used in this chat, also check each one for improvements:
1. If the skill doesn't already have a self-check: add success criteria at the top and an instruction at the bottom to verify those criteria are met before presenting output (iterating up to 5 times if not).
2. Check the skill for conciseness and opportunities to save tokens, without degrading clarity or functionality.
3. Propose any other improvements to the skill, and ask me whether to apply them.

If you notice I repeatedly ask you to do similar tasks, suggest creating a reusable skill and ask for confirmation before doing so.

Also: Proactively suggest typing "reflect" whenever you notice I've had to correct you, clarify something twice, or seem frustrated.

---

When Claude finishes, it should show you the skill and prompt you to click **"Copy to your skills"**. Click it.

**Verify the skill was saved:** Type `reflect`. Since you haven't done any work yet, Claude should explain there's nothing to reflect on but describe what it will do when there is. That confirms the skill is active and will be available in all future sessions.

### How to use it
- Work with Claude normally.
- **When something feels off** – you corrected Claude, re-explained something, or the output wasn't quite right – type:

  `reflect`

Claude will suggest improvements and ask whether to remember them.

**Tip:** If you find yourself explaining the same preference or correction 2-3 times, type `reflect` — Claude will likely suggest creating a skill to remember it.

#### Example
After editing an email together, type `reflect`.
Claude may suggest things like:
- "You prefer concise openings."
- "You care about timezone clarity."

You choose what gets remembered.

#### If something goes wrong
- If `reflect` doesn't work, start a fresh chat and repeat step 3.