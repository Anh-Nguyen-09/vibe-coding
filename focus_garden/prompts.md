# Project: Focus Garden

> - **Files:** focus_garden.html
> - **Dates:** 2026-11-04
> - **Defaults:** Claude · Sonnet 5.5
> - **Status:** prototype
> - **Use:** Built for this assignment as a small study-timer app; not used in any event
> - **Reusability:** artifact medium · prompt pattern high
> - **Tags:** single-file-html, productivity, timer, localstorage
> - **Takeaway:** A one-sentence prompt with clear numbers (1 hour = 1 tree, 10 trees = full garden) was enough for a complete, working app.
> - **Story value:** anecdote
> - **Surprises:** The first version drew the front-row trees over the back row; the assistant caught it in a screenshot and shrank the trees. A later message asked for a demo mode (9 trees already grown, 1-minute session), which is in the html but not in this prompt file.

Note: this file only includes the first prompt. A follow-up message added the demo mode that is in the final html.

# Prompt 1 (focus garden app):

> - **Tool:** Claude · Sonnet 5.5 · 2026-11-04
> - **Session:** continued · attached: none
> - **Verified:** agent-tested
> - **Human edits:** none

generate me a focus garden growing app. each section (1 hour) complete can grow 1 tree. a total 10 trees make a full garden

## Output 1:

Focus Garden is published. Press Plant a tree to start a one-hour session, and a sapling grows on the next empty plot as the hour passes. When the hour finishes it becomes a full tree. There are 10 plots with 10 different tree types, and when all 10 are grown the garden is full and you can start a new one.

- **Giving up:** if you give up (it asks you to confirm), the sapling wilts and no tree is added.
- **Saving:** the garden is saved in your browser. A running session keeps going if you close the tab, and the tree counts if the hour passes while it's closed.
- **Demo speed:** there's a checkbox that makes a 1-minute session count as an hour, so you can see it work without waiting. Demo trees don't add to the Focus hours total.
- **Testing:** I tested it by fast-forwarding the clock at desktop and phone width. A session grew a tree, the garden filled to 10, a new garden started, and giving up wilted a sapling, with no errors. I haven't run a real full hour.
