# AI Usage Disclosure — Save the Planet by 3S

## Summary

**AI tools were used by our mentors (Paola and Edson) as a technical assistant during development.** The three students (Sol, Sofía, Sara) wrote all video scripts, performed all user testing, conducted the 31-neighbour survey and the 10-family pilot, and made every design decision about the app. AI was used as a learning accelerator for the mentor's technical guidance, not as a replacement for student work.

This disclosure is provided per the 2026 Technovation requirement for AI transparency.

---

## Tools used

| Tool | Vendor | Used for | Used by |
|------|--------|----------|---------|
| Claude | Chatgpt | Thunkable debugging advice, architecture reviews, English language polishing on submission texts, document generation | Mentors (Poala/Edson) |

No other generative AI tools were used in the project.

## What AI WAS used for

1. **Thunkable debugging support** — when a bug appeared (e.g., list variables resetting between screens, DVL not refreshing with filter, locale corruption of coordinates), the mentor asked Claude to help narrow down the cause and to suggest diagnostic steps. The fixes themselves were implemented by the students on their own.
2. **Architecture review** — the mentor described the chunk-manifest approach and other design choices to Claude, and asked whether the approach was sound. Claude's responses were treated as one perspective among several, not as authoritative.
3. **English language polish on submission texts** — because the students' working language is Spanish, the mentor used Claude to refine the English wording of video scripts and platform submission texts. Content, numbers, and claims were all student-authored; AI only helped the phrasing.
4. **Document generation** — the submission package `.docx` and this judges package were drafted with Claude's assistance from source materials (pitch scripts, technical scripts, competition package notes) that the team had already produced. The mentors reviewed every line before submission.

## What AI was NOT used for

- **Writing the app code (Thunkable blocks)**: Sofía built every block herself.
- **Writing the video scripts**: Sara led the writing, with Sol on data and Sofía on technical accuracy.
- **Making design decisions**: The 5-screen architecture, the Fibonacci milestones, the Animal Crossing aesthetic, the song, the letters to the Mayor — all student decisions.
- **Cleaning the dataset**: Sol (team/mentors) did the data work herself, including the coordinate-locale fix.
- **Conducting the survey or pilot**: Sara led the 31-neighbour survey and the 10-family pilot, with Sol on data capture.
- **Generating fake or synthetic data**: Every number in our materials is traceable to a real source (the survey, the pilot, the open data portal, or a public statistic from Ecoembes/BOE).

## How AI outputs were validated

The team followed a "check-every-suggestion" rule:

1. Any AI suggestion was written down by the mentor.
2. The relevant student (Sofía for code, Sol for data, Sara for narrative) reproduced the fix or the reasoning on their own.
3. Only if the student could explain the suggestion in her own words was it kept in the project.
4. If a suggestion did not work, it was discarded — several did not work and are listed in `LESSONS_LEARNED.md` (e.g., Thunkable AI Helper generating unsupported block types).

This is the same standard we would apply to any tutorial or Stack Overflow answer. AI was treated as one external source among others, not as an authority.

## Sample of what we asked

To make this disclosure concrete, here are the categories of prompts the mentor used during development (paraphrased; not verbatim):

- "In Thunkable, my list variable is empty after I navigate to a new screen. What could cause this?" — led to discovery of L1 (stored vs app variables).
- "A Filter View update is not refreshing my Data Viewer on some devices. What else could be wrong?" — led to L7 (DVL visible before filter).
- "Spanish Excel is corrupting my latitude column. How do I prevent this at the file level?" — led to L17 (text columns + pre-built URL).
- "Please rewrite this Spanish paragraph in natural, competition-appropriate English" — standard translation polishing for submission texts.

All such interactions were in service of helping the students move faster on their own work, not in producing work in their place.

## Our position on AI in a student competition

We believe AI is a legitimate learning tool when used transparently and when the learner retains ownership of the understanding. Three tests we applied throughout the project:

1. **Can the student explain it?** If Sofía cannot explain why a block works, we do not use it.
2. **Can the student reproduce it?** If Sol cannot rebuild a dataset from the source, the dataset is not hers.
3. **Is it honestly labelled?** If AI helped with wording, we say so — here.

*Code & Shine · Save the Planet by 3S · Technovation Girls 2026*
