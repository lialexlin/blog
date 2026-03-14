---
layout: post
title: Your Obsidian Vault Doesn't Need Better Prompts. It Needs Schema.
date: 2026-03-14
---

You've been using Obsidian + Claude Code wrong. Claude keeps generating garbage properties. Your graph is a mess. You throw more instructions at it. It still gets it wrong.

This is a data modeling problem, not a prompt engineering problem. No amount of instructions will fix a vault with no structure. You need schema.

### Templates are your schema

Obsidian's real power for agents is templates.

Templates predefine the YAML frontmatter for every new note - fixed properties, fixed value types. Claude stops hallucinating properties because the schema already exists.

Every note you'll ever create is one of two things:

**Entities** - things that persist and rarely change. Companies, people, projects.

**Events** - things that happen. A meeting, a piece of research, a thought. Timestamped, linked to the entities they touch.

I use 6 templates total. Three entity types, three event types. If something doesn't fit one of these, I probably don't need it.

### One sentence builds your entire graph

Wiki-links are more flexible than Notion's table-to-table relations. But your agent doesn't know what to link to what.

The fix: every file gets a one-sentence summary as its first line of body content, naming linked entities in wiki-link format:

> Overview of the \[\[XX deal\]\], from discussion with \[\[Bob\]\] at \[\[YY Conference\]\].

That one sentence includes all the most important wiki-links about your note, and builds your graph automatically. No manual linking, no broken connections.

### The setup takes 5 minutes

**One-time:** Define your primitive templates. What are the 5-8 types of things that will ever exist in your vault? Not 20. Not "I'll add more later." Constraints are the point. Make the names self-explanatory so Claude picks the right one from context.

Then add one line to your CLAUDE.md: "After creating a note, prepend a one-sentence summary that names all key entities in wiki-link format." That single instruction turns every new file into a graph node automatically. Structure is automated, judgment stays yours.

**Every new note:** Claude follows this flow.

```bash
obsidian templates                                    # see your templates
obsidian create name="My Note" template="Note"        # create with schema
obsidian prepend file="My Note" content="..."         # prepend the summary
```

The summary lives in the body where wiki-links actually work, not in frontmatter where they're dead text. Properties get populated through the CLI, not by Claude guessing what YAML to write.

Open your terminal and run `obsidian templates` right now. If you see more than 10, start cutting.
