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

## Desktop dashboards (learned building a tracker dashboard as a single HTML file)

28. **White and calm is the default.** The person asked for a white background and "less overwhelming" several times. Add whitespace and margins first. Drop font sizes a notch. Remove borders that aren't doing a job, and use soft tinted fills (`--soft`) to separate areas instead.
29. **Limit colour to a blue/gray/green family.** Colour carries meaning (status), so every extra hue read as noise. Mood art, doodles and icons should reuse the same palette. If a reference image is colourful, borrow the shapes and not the colours.
30. **Keep chrome minimal.** Remove view toggles that aren't wanted. Keep one Filter button with a count badge. Put the stats in a profile sidebar and keep them off the main page until there is good inspiration for them.
31. **Hide secondary panels behind the profile button.** A permanent sidebar crowded the table. A right-hand drawer that opens from the profile avatar (with a faint backdrop, Esc and outside-click to close) kept the table wide. Keep the avatar button to avatar and name only, with no subtitle or chevron.
32. **Put each edit where the work happens.** Owner changes belong in the table row (an Owner column), not on the detail page. Contacts belong with Communications. Put the most actionable block first (Engagement before events, Activity before contacts).
33. **Match tab order to workflow and centre the tabs.** Use a sliding underline plus a slide-in of the content in the direction of travel. Don't re-render the whole page for a tab change.
34. **Make a timeline look like a timeline.** A dotted vertical connector with an icon dot per event (like LinkedIn experience) works. Upcoming items get dashed-outline dots, and past items get filled dots.
35. **Sibling cards must match.** Side-by-side cards use `align-items:stretch` with equal columns, and the inner textarea flexes to fill. Otherwise it reads as a bug.
36. **Make the detail page look full, not empty.** A big avatar header, three summary tiles (stage, next up, last activity) and a clear first card fixed the "looks empty" complaint. Don't just add more fields.
37. **Characters add warmth if they have a job.** Mood faces on stages (blue only; grey out upcoming stages, enlarge the current one) and doodle buddies peeking from the edge of stat cards (clipped by `overflow:hidden`, a short staggered slide-up, a small hover lift) made the app feel friendly. Draw them yourself as simple SVG in the app's palette instead of tracing the reference, and keep motion quiet.
38. **Respect the data in "stat" cards.** Count real things the person cares about (scoping pods, emails, calls) and keep cards small. Say plainly when a count is 0 because there is no sample data yet.
39. **Order and naming come from the user's words.** Rename stages exactly as asked ("Completed", not "Project Completed"). Follow requested orders (scoping pod, email, call). Don't "improve" them.
40. **Make layout changes through data, with Undo.** Projects with links (label, URL, open ↗ with `https://` added automatically, `rel=noopener`) migrated from the old single-project field. Deleting shows an Undo toast instead of a confirm dialog.

## Visual language (concrete design choices from a tracker dashboard)

Use these as starting values for a calm, modern, light-theme dashboard. Change them only with a reason.

**Colour tokens** (define on `:root`, light theme only unless asked)
- Background `#fff`. Soft fill for cards, search and ghost buttons `#f5f7fb`, with a slightly darker `#eceff6` for dividers.
- Text: ink `#16213a`, secondary `#586580`, tertiary `#8c97ab` (labels, helper text, column headers).
- One accent blue `#3f6fd9` (hover `#2f5bc0`, tint `#e9effe`). Green `#23804a` on `#e3f5ea` only for "done / success". Gray `#6b768b` on `#eef1f6` for "not started".
- Status meaning by hue: gray = not started or waiting, blue = in progress, green = reached or delivered. No red, orange or purple.

**Type**
- Inter (system fallback). Base 13.5px / 1.5. Small labels 12–12.5px. Column headers 11.5px uppercase, weight 600, letter-spacing .05em, in tertiary ink.
- Headings and wordmark: weight 700, letter-spacing -.035em. Page title 26px in the accent blue. Org name on detail page 24px in ink. Section headings 15–16px.
- Inputs 16px on mobile, matching text on desktop.

**Shape and spacing**
- Radius scale: pills 999px, buttons 12px, inputs 10–12px, rows 16px, cards 24px (28px for the big drawer's outer edge). Don't mix other values.
- Cards are a soft fill with no border and no shadow. Shadows are reserved for floating things (menus, drawer), and they stay very soft: `0 14px 40px rgba(22,33,58,.14)`.
- Page max-width about 1176px with 48px side padding. Generous gaps: 28px between cards, 36px under the page title, 40px above tabs. 38px control height, 30px for pills.
- Tables are rows with no cell borders. A row gets a soft hover fill. Use a grid with `minmax()` columns, give pills enough width so labels never truncate, and let long text (email, location) ellipsise.

**Components**
- **Dropdowns** are coloured pills (dot + label + small chevron that rotates when open), opening a floating menu with soft shadow, a check mark on the selected item, and keyboard navigation.
- **Primary button** is solid blue with white text. Secondary is the soft fill. Only one primary per row.
- **Filter** is one button with a count badge. It opens a popover (bottom sheet on phones) with multi-select chips.
- **Summary tiles** (stage / next up / last activity) are soft cards with a white rounded icon square, a tiny uppercase label, a bold value and a muted detail line.
- **Profile** is just an avatar and a name. Clicking opens a right drawer with a big initials badge, "Hello, Name!" (name in bold), small stat cards, then the weekly calendar and an upcoming list.
- **Empty states** are one emoji or doodle, a bold line and one sentence. They never look like errors.
- **Toasts** sit at the bottom with an Undo action for deletions.

**Motion**
- 0.15s for hovers and 0.2s for fades. 0.3s with `cubic-bezier(.2,.7,.3,1)` for slides (tabs, drawer, doodles). Press feedback is `scale(.92–.97)`. Confetti only on a real milestone (a stage reaching "Completed").
- Always honour `prefers-reduced-motion`.

**Illustration**
- Stage moods: six simple blob faces, blue shades only, with the current one larger and the rest grey until hovered, joined by a dotted line that turns blue as it progresses.
- Stat doodles: a rounded bean character in 2px navy line-art on white, holding an object tinted with the accent (envelope, phone), peeking from the bottom-right of the card.
- Icons are simple 1.8px line icons. Emoji icons looked "weird" and were removed.

### Verifying a single-file HTML app without a device
- Run `node --check` on the extracted script after every patch.
- Copy the file, inject test code that clicks through the UI and writes JSON into `document.title`, and read it with headless Chrome `--dump-dom`. Test the behaviour you changed and one older behaviour.
- Take screenshots with `--force-prefers-reduced-motion` so animations don't blur them, and look at them before reporting. They caught truncated columns, empty cards and unequal heights.
- Apply edits as small patch scripts (Python with `-I`) and check each replacement for a "MISS" message. A silent miss means the change didn't happen.


## Micro animations

Small motion makes an app feel alive, but only if it is quick, purposeful and stops by itself. Every animation below earned its place; anything else was cut.

- **Hover and press feedback (0.1–0.15s).** Buttons and pills darken or tint on hover and shrink to `scale(.92–.97)` while pressed. Icon buttons get a soft tinted background. This is the one place motion is allowed everywhere.
- **Fades for arriving content (0.2s).** A page or list fades in once on entry. Rows can stagger by index (about 20–30ms each, capped at about 10 rows) so a long list doesn't take a second to appear.
- **Slides for direction (0.3s, `cubic-bezier(.2,.7,.3,1)`).** Tab content slides in from the side you're moving towards (40px with a fade). A drawer slides in from its own edge. Use a sliding underline (animate `transform` and `width`) for the active tab rather than redrawing it.
- **Pop for small floating things (0.14–0.2s).** Menus and badges scale in from their anchor corner (`transform-origin` at the trigger). A chevron rotates 180° when its menu opens.
- **Checkmarks and states fade and scale in (0.18s).** The selected item's tick goes from `scale(.7)` and invisible to full size. A copy button swaps to a tick for about 1.4s, then back.
- **Peek animations for illustrations.** A doodle sliding up from the card edge (30px, 0.5s) with a 70ms stagger between cards, then a 4px lift on hover. It plays once when the panel opens and then stays still.
- **Celebrate rarely.** Confetti only when something genuinely finishes (an item reaches its final stage). Never for routine saves.
- **Animate only `transform` and `opacity`.** They stay smooth and don't shift the layout. If something must change size, change it instantly and fade the content.
- **Honour `prefers-reduced-motion`.** Wrap or disable all of the above. It also makes screenshots in tests stable (headless Chrome: `--force-prefers-reduced-motion`).
- **No idle motion.** Nothing bounces, pulses or loops while the person is just reading.

## Icons

- **Use one family, one stroke.** A mixed set looks messy. The best-looking result was simple outline icons: 24px viewBox, `stroke="currentColor"`, `fill="none"`, 1.6–1.8 stroke width, round caps and joins. Lucide and Feather follow exactly this style; Lucide (ISC licence, actively maintained) is the one to reach for.
- **Single-file apps: inline only the icons you use.** Copy each icon's SVG paths into a small map (`{ search: '<circle…/>', plus: '…' }`) and render with one helper `ico(name, size)`. This keeps the file self-contained with no network or build step. Don't load a whole icon font or CDN set for ten icons.
- **Apps with a build step: use the library's own package** (for example `lucide-react`) and import icons one by one so unused ones are tree-shaken out.
- **Let icons inherit colour.** With `currentColor`, an icon automatically matches hover, disabled and accent states. Tint the container (a soft blue square behind the icon) rather than recolouring the glyph.
- **Size by context.** 14–15px inside small buttons and dropdown chevrons, 16–18px next to labels, 20–22px in tiles, and no larger than that inside rows.
- **Icon-only buttons need a name.** Add `aria-label` (and `title` where hovering helps), and a hit area of at least 32px even if the glyph is 15px.
- **Avoid emoji as UI icons.** They looked "weird" next to a clean type system and vary across devices. Emoji is acceptable only in an empty state, as one friendly illustration.
- **Use meaning, not decoration.** Re-use the same icon for the same thing everywhere (mail = email, phone = call, calendar = meeting), and drop the icon when the label alone is clear.
- **Custom art is separate from the icon set.** Mascots, mood faces and doodles are illustrations: draw them as their own SVGs in the app's palette, and don't mix them into the line-icon set.

## Checklist before saying a UI is done

- [ ] Anything on screen that isn't needed?
- [ ] Every control tappable directly, with common actions always visible?
- [ ] One job per gesture, with strict thresholds?
- [ ] Text and input sizes consistent? Inputs don't trigger iPhone zoom?
- [ ] Motion is a single quiet fade or glide, and it stops?
- [ ] Safe areas, keyboard, and drop targets handled?
- [ ] Panels grow with content and have a cap?
- [ ] What was and wasn't tested on a real device is stated plainly?
- [ ] White background, only blue/gray/green colours, no borders that don't do a job?
- [ ] Sibling cards the same size, and the first card is the most useful one?
- [ ] Every edit lives where the person does that job (owner in the table, contacts in Communications)?
- [ ] Animations only use transform and opacity, are under about 0.3s, and respect reduced-motion?
- [ ] One icon family with one stroke width, using currentColor, with labels on icon-only buttons?
