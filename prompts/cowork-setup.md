# Getting Claude to Improve Over Time (Simple Setup)
Frustrated at having to copy/paste prompts all the time, or seeing Claude making the same mistakes? Here's a quick guide to have a **self-improving setup for Claude.** Great for non-technical users.

## 1) Install & basic privacy
- Install **Claude Desktop:** [claude.com/download](https://claude.com/download)
- Open **Settings → Privacy** and deselect **"Help improve Claude"** so your conversations and preferences remain private.

## 2) Start a chat
Open Claude Desktop, then:
- **If you have a paid plan:** Click **"Cowork"** at the top, then start a new chat. You'll see a prompt to select a folder. I suggest creating a "Claude" folder in your home folder (for example, `Users/yourname/Claude`).
- **If you're on the free plan:** Start a regular chat. Then **(very important)** paste the following and send the message: 
  >Add this to your memory: Every time you create or edit a skill, you must use the present_file tool to show me the finished skill, and clearly tell me to click "Copy to your skills" to save it. Warn me that the skill will be lost if I don't click that button.

*This guide works best with a paid plan and Cowork mode. The free plan's chat mode is still usable, though the experience is slightly less seamless.*

## 3) Create the "reflect" skill
A **skill** is a saved instruction that Claude remembers across all your future chats. It's the basic building block to ensure that Claude gets better as you keep using it.

Copy-paste this in your chat with Claude:

> Create a skill called "reflect".
> When I type "reflect", you should:
> 1. Review what we've done in this chat.
> 2. Identify mistakes, friction, or unclear outputs.
> 3. Propose a short list of concrete improvements.
> 4. Ask me which of these you should remember for future chats.
>
> If any skills were used in this chat, also check each one for improvements:
> 1. If the skill doesn't already have a self-check: add success criteria at the top and an instruction at the bottom to verify those criteria are met before presenting output (iterating up to 5 times if not).
> 2. Check the skill for conciseness and opportunities to save tokens, without degrading clarity or functionality.
> 3. Propose any other improvements to the skill, and ask me whether to apply them.
>
> If you notice I repeatedly ask you to do similar tasks, suggest creating a reusable skill and ask for confirmation before doing so.
>
> Also: Proactively suggest typing "reflect" whenever you notice I've had to correct you, clarify something twice, or seem frustrated.

Then, depending on the interface you are using:

**- If you are using the Chat interface:** When Claude shows the new skill file, click **"Copy to your skills"** to save it.

**- If you are using the Cowork interface:** The skill is saved automatically.

**Verify the skill was saved:** Ask Claude to "Show me the skills you have available." The newly created "reflect" skill should be there. If not, you may want to re-read the previous steps carefully to ensure you haven't missed anything. In particular, make sure that, if Claude asked you if you wanted to save the newly created skill, you answered affirmatively, and if he showed you a "Copy to your skills" button, you did click on it. In the remote event this is not sufficient, simply ask Claude to "help me save the reflect skill so that it's available in new sessions."

### How to use it
At the end of each work session, or milestone, type reflect and send the message. Then let Claude self-improve.

To edit skills, simply describe the required change to Claude, and he will assist you.

---

*This guide is provided as-is for informational purposes only. AI tools may produce inaccurate or unexpected outputs. Always review results before acting on them. See the project [LICENSE](https://github.com/lucadellanna/luca-skills/blob/main/LICENSE) for full terms.*
