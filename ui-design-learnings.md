---
name: ui-design-learnings
description: Design and build calm, mobile-first UIs (especially touch web apps and PWAs). Use when designing or building an app screen, adding gestures, drag and drop, bottom sheets or text inputs, or when reviewing a UI against these rules. Distilled from building a mobile-first planner app.
---

# UI design learnings

Rules for building calm, mobile-first UIs. Apply them when starting a UI or reviewing one. Each rule says what to do; the "why" is there so you can judge edge cases.

## Design principles

1. **Subtract before you add.** Most useful feedback was "remove this". Before adding a label, button or caption, ask if the screen works without it. Cut anything that isn't needed.
2. **Make the thing itself the control.** If a labelled element can be tapped, let it work directly (tap a category pill to open it, tap again to close). Don't add a separate +/- button next to it.
3. **Always show common actions.** A small, always-visible × is clearer than a button that appears after a tap. Visible beats clever.
4. **Give each gesture one job.** For example: tap edits, double-tap completes, swipe right adds a child item, press-and-hold then drag moves. Keep thresholds strict (mostly sideways, enough distance) so scrolling never triggers a gesture.
5. **Keep motion quiet.** Use one soft fade or glide. No bouncing, pulsing or idle animation. Let transitions finish and then stop. Don't animate mascots or decorations.
6. **One size per kind of text, including inputs.** An editing field must match the text it edits. A field that looks bigger than its content reads as a bug.
7. **Soften hard edges.** A pinned or sticky element needs a subtle fade or margin under it. Keep it subtle: if the person notices it, it's too strong.
8. **Keep things in predictable places.** New items go at the bottom of a list. The same card looks and behaves the same everywhere.
9. **Reuse patterns the person already knows.** A new area (such as a side panel for ideas) should look and work like an existing one (subtasks, swipe, double-tap) so there is nothing new to learn.
10. **Limit the palette.** Pick about four colours and use tints of them. Keep one accent colour for one meaning.
11. **Give decoration a job.** A mascot is better as the bin or a status than as an extra ornament.

## Mobile and touch

12. **Test on the real device early.** The serious bugs (blank screen, slow load, drag that won't drop, keyboard covering the input) never showed up on a laptop. Treat laptop checks as partial.
13. **Weight is a design choice.** A small bundle that opens fast beats polish. If load time annoys the user, change the stack before changing the screens.
14. **Inputs under 16px make iPhone Safari zoom in.** Either use 16px, or block page zoom (`maximum-scale=1`) and size inputs to match the surrounding text.
15. **Plan for the keyboard.** iPhone keeps the page at full height when the keyboard opens and hides the bottom. While it is open, size the app to `visualViewport.height`, hide non-essential bars (such as the tab bar), and scroll the active field into view after about 350ms.
16. **Respect safe areas.** Use `env(safe-area-inset-top)` and `env(safe-area-inset-bottom)`, and fill the top space with the background colour.
17. **Fingers are not mice.** A finger can't separate scrolling from dragging, so use press-and-hold (about 320ms) before a drag. Safari may cancel pointer events once it thinks the finger is scrolling, so also handle the drop through `touchend`, ignore `pointercancel`, and block page scroll with a non-passive `touchmove` while dragging.
18. **Don't block drop targets.** If items can be dragged onto something, keep that target visible. Keep panels that open over the screen short.
19. **Let panels grow with their content, up to a cap.** A fixed height runs out of room (a 30% panel left no space for a new subtask). Use auto height with a `max-height` (around 45% worked well), and scroll the list inside it past that.
20. **Stop the page scrolling under overlays.** Use `overscroll-behavior: contain` on inner scrollers and hide scrollbars.
21. **Dictation:** browser speech recognition often doesn't work in an iPhone home-screen app. Offer the mic, but show a message pointing to the keyboard's own mic when it fails.

## Process

22. **Decide small things and say so.** Make the obvious choices yourself and mention them in your report, so the person can undo what they dislike instead of answering a list of questions.
23. **Work in small steps.** Short, specific changes are easy to check and easy to reverse. Rebuild and push after each.
24. **Report what you verified and what you didn't.** Separate "tested in a browser", "simulated" and "not tested on the device", and ask the person to try the device.
25. **Fix the cause, not the symptom.** A font that looks too big may be an iPhone rule, not a CSS value. A drag that can't drop may be a cancelled event, not a missing handler.
26. **Choose tools around the person's constraints.** If they won't pay for a developer account, don't build on a stack that needs one.
27. **Test side effects.** After changes, check that old behaviour still works (for example, that mouse drag still works after fixing touch drag), and clear any test data you added.

## Checklist before saying a UI is done

- [ ] Anything on screen that isn't needed?
- [ ] Every control tappable directly, with common actions always visible?
- [ ] One job per gesture, with strict thresholds?
- [ ] Text and input sizes consistent? Inputs don't trigger iPhone zoom?
- [ ] Motion is a single quiet fade or glide, and it stops?
- [ ] Safe areas, keyboard, and drop targets handled?
- [ ] Panels grow with content and have a cap?
- [ ] What was and wasn't tested on a real device is stated plainly?
