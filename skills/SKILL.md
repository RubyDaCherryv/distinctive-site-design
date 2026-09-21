---
name: distinctive-site-design
description: Designs and builds distinctive, visually cohesive websites and landing pages that do not look like generic AI templates, choosing a visual direction that fits the site's goal (sales landing, brand/image page, business-card or portfolio site, event, product showcase) and making the layout adapt to iPhone Duo (Apple's foldable phone) as well as ordinary phones, tablets and desktops. Use this skill whenever the user asks to design, build, restyle or redesign a website, landing page, one-pager, portfolio or any frontend UI, even if they only say "make me a nice site", and whenever foldable, iPhone Duo, fold, hinge, dual-screen or compact/expanded-screen responsiveness comes up.
---

# Distinctive Site Design

Goal: every site this skill produces should look like it was designed for one specific subject and one specific job, not pulled from a template. The skill combines two open-source sources and Apple's own guidance:

| Source | What this skill takes from it | Where |
|---|---|---|
| Anthropic `frontend-design` skill (anthropics/claude-code, plugins/frontend-design) | The design process: pin the subject, brainstorm a token plan, critique it against defaults, build, critique again; the "signature element" idea; restraint; copy as design material | Steps 0-6 below, `references/design-principles.md` |
| `mirzaaghazadeh/iphone-duo-skills` | Device facts, size classes, poses, fold/reserved-region logic, "branch on space, not on orientation or idiom" | `references/iphone-duo.md` |
| Apple, *Designing for iPhone Duo* (HIG) and the iPhone Duo Tech Talks | The primary source behind the Duo rules | `references/iphone-duo.md`, `references/sources.md` |

Reply to the user in the language they write in. Keep code, file names and CSS in English.

## Workflow

Do the steps in order. Do the planning silently or in a compact block; show the user the chosen direction and the reason, not every discarded idea.

### Step 0. Pin the brief

If the brief leaves any of these open, decide them yourself and state the decision in one line each:

- **Subject**: one concrete thing (a bakery in Lisbon, a cardiology clinic, a modular synth maker), not a category.
- **Audience**: who lands on this page and what they already know.
- **Single job of the page**: sell, impress, introduce, book, explain, recruit.
- **Real content**: use the brief's real names, numbers, materials and vocabulary. If none exist, write specific, plausible copy from the subject's own world. No lorem ipsum, no "Empower your workflow".

The subject's own world (materials, instruments, artifacts, jargon) is where distinctive visual ideas come from.

### Step 1. Classify the goal and read the matching direction guide

Open `references/goal-directions.md`. Find the site type (sales landing, image/brand page, business card/portfolio, event, product showcase, editorial/content, or a hybrid) and note its page job, hero thesis, structure and density. A goal changes the layout logic, not only the colors: a sales page needs a persuasion sequence, an image page needs atmosphere and pacing, a business card needs fast scanning.

### Step 2. Explore three directions, pick one

From the direction library in the same file, write three candidate directions as one line each: name, why it fits this subject, what it risks. Pick the one that fits the subject best, not the one you would pick for every project. Use the inspiration galleries listed in `references/sources.md` only to study patterns (composition, type, pacing). Never reproduce one existing site.

If the user's brief already pins a direction, follow it exactly. The brief's words win over this skill.

### Step 3. Write the design plan (tokens)

Keep it compact:

- **Color**: 4-6 named hex values with roles (ground, ink, accent, and so on).
- **Type**: at least two roles: a characterful display face used with restraint, a body face, and a utility face for labels or data if needed. Set a type scale with deliberate weights and spacing.
- **Layout**: one sentence of concept plus a small ASCII wireframe of the hero and one other section, at two widths (compact and wide).
- **Signature**: the one element the page will be remembered by, tied to the subject.
- **Motion**: what moves, why, and what stays still.

### Step 4. Critique the plan, then revise

Compare the plan with what you would produce for any similar page. Check it against `references/design-principles.md`, section "Defaults to avoid". If any part reads as a default, change it and say in one sentence what changed and why. Only then write code.

### Step 5. Build

- Follow the revised plan exactly; derive every color and type decision from it (CSS custom properties).
- Use the framework and delivery format the user asked for. If unspecified, produce a self-contained `index.html` with inline CSS and minimal JS.
- Apply the responsive and iPhone Duo rules from `references/iphone-duo.md` from the first line of layout code, not as a patch at the end.
- Watch selector specificity so section and component rules do not cancel each other (typical failure: spacing set on `.section` overridden by an element selector).
- Quality floor, met without announcing it: works from compact phone to desktop, visible keyboard focus, `prefers-reduced-motion` respected, real contrast, semantic HTML, meaningful alt text.

### Step 6. Verify and report

- If the environment can render pages, screenshot at the widths listed in the Duo reference and fix what breaks. If it cannot, walk the checklist in `references/iphone-duo.md` against the code.
- Remove one accessory: cut a decoration that does not serve the brief.
- Tell the user, in a few lines: the subject and job you assumed, the direction you chose and why, the signature element, and any Duo behavior you could not verify.

## Ground rules that apply to every site

- One bold decision, everything around it disciplined. Spend the risk in one place.
- Structure encodes information. Use numbering, eyebrows, dividers and labels only when they say something true about the content (numbered steps only for a real sequence).
- Hero is a thesis: open with the most characteristic thing in the subject's world (image, headline, live demo, interaction), not a big number plus gradient by default.
- Animation is optional. An orchestrated moment beats scattered effects; extra motion makes a page feel machine-made.
- Copy is design material: specific over clever, active voice, controls named by what they do, the same action keeps the same name everywhere.

## When something is unclear

Prefer making a reasoned choice and stating it over asking many questions. Ask at most one question, and only when the answer would change the whole direction (for example, a sales page versus an image page for the same business).
