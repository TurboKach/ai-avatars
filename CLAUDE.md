# AI Avatars Project

## Project Purpose

A curated collection of AI debate avatar personas stored in `avatars_debate.md`. Each avatar is a character with a unique debate style, enriched with Wikidata metadata (portrait images and voice samples from Wikimedia Commons).

## Avatar Entry Format

Every avatar in `avatars_debate.md` MUST follow this exact structure:

```markdown
### **Name: [Character Name]**

**Wikidata:** [QID](https://www.wikidata.org/wiki/QID)
**Description:** One-line personality summary ending with period.
**Prompt:** System prompt with {topic} placeholder. MUST include "IMPORTANT: Respond in 1–2 sentences only" constraint.
**Image:** Wikimedia Commons URL or _Not available on Wikidata_
**Voice Sample:** Wikimedia Commons URL or _Not available on Wikidata_
```

Entries are separated by `---` with blank lines above and below.

## How to Add New Avatars

### Step 1: Write the avatar entry manually

For each new persona, write:
- **Name**: Display name (use quotes for nicknames, e.g. `Dwayne "The Rock" Johnson`)
- **Description**: Under 10 words. Format: `[Adjective] [noun] of [key trait] and [key trait].`
- **Prompt**: Follow this template:
  ```
  You are [Name], an AI debate opponent. You speak with [2-3 style traits]. You are debating the user on the topic: '{topic}'. IMPORTANT: Respond in 1–2 sentences only. [2-word style summary].
  ```

### Step 2: Enrich with Wikidata

Use the Wikidata API to find and attach metadata:

1. **Search for the entity:**
   ```
   GET https://www.wikidata.org/w/api.php?action=wbsearchentities&search=NAME&language=en&format=json
   ```
   - Pick the correct QID from results. IMPORTANT: For fictional characters and ambiguous names, verify the description matches (e.g. "Batman" returns a Turkish province first — you need Q2695156, the DC Comics character).

2. **Fetch entity claims:**
   ```
   GET https://www.wikidata.org/w/api.php?action=wbgetentities&ids=QID&props=claims&format=json
   ```

3. **Extract these properties:**
   - **P18** (image) → Convert filename to: `https://commons.wikimedia.org/wiki/Special:FilePath/FILENAME` (replace spaces with underscores, URL-encode)
   - **P990** (voice recording) → Same URL format as above
   - If P990 is empty, also check the entity's Commons category (P373) for audio files

4. **Known tricky QIDs for fictional/ambiguous characters:**
   | Character | Correct QID | Wrong match to avoid |
   |-----------|-------------|---------------------|
   | Batman | Q2695156 | Q80370 (Turkish province) |
   | Hulk | Q188760 | Q76547 (Nico Hülkenberg) |
   | Yoda | Q51730 | Q8054264 (genus of worms) |
   | Mary Poppins | Q3735317 | Q209170 (the 1964 film) |
   | Tyler Durden | Q4001141 | Q110740078 (Czech rapper) |
   | Cleopatra | Q635 | Q18002300 (given name) |
   | Marie Antoinette | Q47365 | Q20154678 (given name) |

### Step 3: Rate-limit API calls

Use 300ms delay between Wikidata API requests. Set `User-Agent` header.

## Voice Sample Availability

Most voice samples on Wikidata (P990) are limited to:
- Politicians with public speeches
- Historical figures with archived recordings
- A few contemporary public figures

For celebrities, musicians, and fictional characters, Wikimedia Commons generally does NOT host voice samples (copyright). Mark these as `_Not available on Wikidata_`.

## Quality Checklist for New Avatars

- [ ] Name matches a recognizable public figure or fictional character
- [ ] Wikidata QID is correct (verified label + description)
- [ ] Prompt contains `{topic}` placeholder
- [ ] Prompt contains "IMPORTANT: Respond in 1–2 sentences only"
- [ ] Image URL loads a relevant portrait (test in browser)
- [ ] Voice sample URL loads audio (if available)
- [ ] Entry ends with `---` separator
