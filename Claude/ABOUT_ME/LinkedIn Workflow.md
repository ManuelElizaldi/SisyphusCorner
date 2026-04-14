Read all files in ABOUT_ME/ and TEMPLATES/linkedin-angle.md.
I want to write a LinkedIn post about [topic].
Follow the template — ask me the clarifying questions before doing anything else.
# LinkedIn Short Post Workflow

## Overview

Three steps inside Claude Code + one outside. Angle to posted in under an hour.

---

## Setup

```bash
cd /mnt/remotessd/claude-context/
claude
```

Claude Code reads CLAUDE.md and all files in ABOUT_ME/ automatically.

---

## Step 1 — Find the angle

```
Read all files in ABOUT_ME/ and TEMPLATES/linkedin-angle.md.
I want to write a post about [topic]. Ask me the clarifying questions.
```

Answer the 5 clarifying questions honestly and specifically. The quality of your answers here determines everything downstream. Do not rush this step.

---

## Step 2 — Generate hooks

```
Now use TEMPLATES/linkedin-hook.md to generate 
10 hooks for this post.
```

10 variations across 5 techniques. Pick 1-2 you like. Claude Code will flag the 2 strongest and explain why. Final call is always yours — pick what feels true to your voice.

---

## Step 3 — Write and save

```
Use the angle and hook I picked. Apply writing-style.md.
Save the draft to OUTPUTS/linkedin/[post-name].md
```

Review against your 5 commandments before approving. Especially #3: did it actually go there, or describe going there?

---

## Step 4 — Build the visual (outside Claude Code)

1. **Pinterest** — search `[topic] infographic` or `[topic] cheat sheet` Download the best content structure reference
    
2. **Gemini** (gemini.google.com, Thinking model on) Upload Pinterest image and run:
    
    ```
    Extract all of the information from this infographic so another 
    designer could remake it. Your goal is to brief it, as if the 
    designer was Gemini nano-banana (reverse prompting).
    ```
    
3. **Pinterest again** — search `handwritten style infographic` Download a scrappy, non-corporate style reference
    
4. **Gemini follow-up** — upload style reference and run:
    
    ```
    Now remake this infographic with the information you just extracted, 
    but using the style of the image I just uploaded. 
    Copy only the style — content comes from your previous extraction.
    Make it 1080 x 1350 pixels, portrait orientation.
    ```
    
5. **Clean up** — if decorative elements remain:
    
    ```
    Strip everything that isn't the core diagram, labels, and arrows.
    Clean white or light paper background only.
    ```
    
6. **GIMP** — if Gemini leaves a watermark or signature:
    
    - Open image in GIMP
    - Press `C` for Clone Stamp tool
    - `Ctrl + click` a clean background area near the signature
    - Paint over the signature
    - `File → Export As → .png`

---

## Step 5 — Post to LinkedIn

- Upload infographic as image
- Paste post text
- Add hashtags: `#AWS #DataEngineering #CloudComputing #LearningInPublic`
- Best days: Tuesday, Wednesday, Thursday morning

---

## Step 6 — Track performance

After 48 hours note:

- Impressions
- Followers gained
- Comments / saves

This becomes your baseline. Over time you'll see which angles and hooks move the needle.

---

## Quick reference — hook techniques

|Technique|Structure|
|---|---|
|Contradiction|"The [expected thing] actually [unexpected outcome]."|
|Specific number + context|"I [did X with number]. [Surprising result]."|
|Direct accusation|"You're [doing common thing]. [Why it costs them]."|
|Stolen thought|"You already know [uncomfortable truth]. [Validation + pivot]."|
|Absurd reframe|"[Mundane thing] has [absurd stakes]. [Most people miss it]."|

---

## Hard rules (from writing-style.md)

- No personal achievement openers
- No hedging
- No cheesy CTAs
- Short paragraphs, no emojis, no hashtag soup
- Specific over general — always
- Strip every explanation after a strong image
- If it could apply to anyone, rewrite it until it couldn't

---

## Templates location

```
/mnt/remotessd/claude-context/TEMPLATES/
├── linkedin-angle.md
├── linkedin-hook.md
└── linkedin-visual.md
```

## Outputs location

```
/mnt/remotessd/claude-context/OUTPUTS/linkedin/
```