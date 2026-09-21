# Design principles

Distilled and paraphrased from the official Anthropic `frontend-design` skill (anthropics/claude-code, `plugins/frontend-design/skills/frontend-design/SKILL.md`), then extended for this skill. Read the original for its exact wording.

## Contents
1. Posture
2. Defaults to avoid
3. Typography
4. Structure and layout
5. Motion
6. Copy
7. Code hygiene
8. Final self-critique

## 1. Posture

Work like the design lead at a small studio whose clients pay for a point of view. The client has already rejected templated proposals. Make deliberate, opinionated choices for palette, type and layout that belong to this brief, and take one real aesthetic risk you can justify in a sentence.

Match complexity to the vision. Maximalist directions need elaborate, careful execution. Minimal directions need precision in spacing, type and detail. Elegance is executing the chosen direction well.

## 2. Defaults to avoid

AI-generated design currently clusters around three looks. Each is legitimate for some briefs, but each is a default, not a choice:

1. Warm cream ground (near `#F4F1EA`), high-contrast serif display, terracotta accent.
2. Near-black ground with one acid-green or vermilion accent.
3. Broadsheet layout: hairline rules, zero border radius, dense newspaper columns.

Rule: where the brief names a direction, follow it, even if it is one of these three. Where the brief leaves an axis free, do not spend that freedom on one of them. Other recurring tells to check for:

- Purple-to-blue gradient hero with a glass card.
- Big number, small label, three stat tiles in a row, used because it is habitual.
- Three equal feature cards with icons, then a testimonial carousel, then a pricing table, regardless of subject.
- Numbered "01 / 02 / 03" markers on content that is not a sequence.
- Stock adjectives in copy ("seamless", "powerful", "next-generation").
- The same font pairing you would reach for on any project.

A quick test: imagine the page for two unrelated subjects. If only the logo and colors change, the design is a template.

## 3. Typography

Type carries the personality. Pair display and body faces on purpose, and make the type treatment a memorable part of the design. Set a clear scale, intentional weights, widths and spacing. Use a utility face for captions, data and labels when the content has data. Use the display face with restraint.

## 4. Structure and layout

- The hero is a thesis about the subject.
- Structural devices (eyebrows, dividers, labels, numbering) must encode something true about the content.
- Explore layout with ASCII wireframes before code, at both compact and wide widths.
- Give the page one signature element and keep the rest quiet.

## 5. Motion

Decide where and whether animation serves the subject: a page-load sequence, a scroll reveal, hover feedback, ambient atmosphere. One orchestrated moment usually lands harder than many small effects. Always respect `prefers-reduced-motion`. Sometimes the right amount is none.

## 6. Copy

Words exist to make the page easier to understand and use.

- Write from the end user's side of the screen. Name things by what people control and recognize, not by how the system is built.
- Be specific instead of clever. Describe what something does in plain terms.
- Prefer active voice. A button says what happens ("Save changes", not "Submit"). An action keeps one name through the whole flow.
- Errors explain what went wrong and how to fix it, without apology. An empty state invites an action.
- Sentence case, plain verbs, no filler. Each element does exactly one job.

## 7. Code hygiene

- Define color, type and spacing as CSS custom properties from the design plan.
- Avoid selector-specificity collisions (a type-like `.section` class versus element selectors for spacing).
- Use semantic elements, visible `:focus-visible` styles, sufficient contrast.

## 8. Final self-critique

Before delivering: does the hero say something only this subject could say? Is there exactly one memorable signature? Would the page survive a swap of the logo and colors, and if so what makes it specific? What is the one accessory to remove?