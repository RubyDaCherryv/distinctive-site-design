# Sources

## Contents
1. Base skills used
2. Apple material on iPhone Duo
3. Secondary summaries used to cross-check Apple
4. Inspiration galleries (pattern study only)
5. Licenses and attribution

## 1. Base skills used

1. **Anthropic `frontend-design` skill**: https://github.com/anthropics/claude-code/blob/main/plugins/frontend-design/skills/frontend-design/SKILL.md
   Read in full. Used for the process (pin subject, token plan, critique against defaults, build, critique again), the three defaults to avoid, typography and signature-element ideas, motion restraint, and the writing rules. Paraphrased in `design-principles.md`.
2. **iPhone Duo Skills**: https://github.com/mirzaaghazadeh/iphone-duo-skills
   README and `reference/device-facts.md` read. Used for device facts, size classes, poses, and the "branch on space, not on idiom or orientation" principle. Nine native-iOS skills in that repo (readiness, adaptive layout, vertical bars, hinge and scenes, camera, design review, games, Flutter, React Native) were listed but not all read in full; only `device-facts.md` was read in detail. Its `reference/sources.md` lists its own primary sources.

## 2. Apple material on iPhone Duo

- Designing for iPhone Duo (HIG): https://developer.apple.com/design/human-interface-guidelines/designing-for-iphone-duo. Requires JavaScript; could not be read directly. Re-read before relying on exact wording.
- Design for iPhone Duo (Tech Talk): https://developer.apple.com/videos/play/tech-talks/111466/. Source of the guidance to keep interactive elements out of the curve region and that scrollable content need not avoid it.
- Strike a pose with adaptive layouts on iPhone Duo (Tech Talk): https://developer.apple.com/videos/play/tech-talks/111463/. Source for reserved regions and the fold's division region being active only when folded.
- Developer hub: https://developer.apple.com/iphone-duo/

## 3. Secondary summaries used to cross-check Apple

- https://www.sagarunagar.com/blog/iphone-duo-human-interface-guidelines (HIG summary: two size classes, poses, system containers, scrolling content exempt)
- https://blakecrosley.com/blog/designing-for-iphone-duo (asymmetric safe areas, side controls, exempt scrolling content)
- https://bitrig.com/blog/iphone-duo-app-development (reserved regions: division and occlusion)
- https://ecorpit.com/iphone-duo-sdk-new-apis-xcode-27-1-developer-guide-2026/ (native API status; SDK support pending Xcode 27.1)
- https://www.mobilemarketingreads.com/developer-guidance-for-building-apps-for-iphone-duo/ (bars and status elements moving to the side)

These are third-party summaries. Where they disagree with Apple's pages, Apple wins.

## 4. Inspiration galleries (pattern study only)

Listed from general knowledge; not fetched in the session that wrote this skill. Check that each still loads before citing it in a deliverable. Use them to study composition, type and pacing. Never reproduce a site.

- Awwwards: https://www.awwwards.com
- Godly: https://godly.website
- Siteinspire: https://www.siteinspire.com
- Land-book: https://land-book.com
- Lapa Ninja (landing pages): https://www.lapa.ninja
- Httpster: https://httpster.net

## 5. Licenses and attribution

- The iPhone Duo Skills repository is MIT licensed and not affiliated with Apple. "iPhone" and "iPhone Duo" are trademarks of Apple Inc.
- The Anthropic `frontend-design` skill is distributed with its own license (see the repository). This skill paraphrases its ideas and does not copy its text.
- Apple's HIG and Tech Talks are Apple's; this skill only summarizes and links.