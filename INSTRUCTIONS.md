# AI Avatars - Debate Personas

A curated collection of AI debate avatar personas with Wikidata-enriched metadata.

## What is this?

`avatars_debate.md` contains a library of 47 persona definitions for AI-powered debate opponents. Each avatar has a distinct speaking style, personality, and rhetorical approach. They are designed for voice-based AI debate applications where the user argues against a character.

## Avatar Entry Format

Each entry follows this structure:

```markdown
### **Name: [Character Name]**

**Wikidata:** [QID](link)
**Description:** One-line personality summary.
**Prompt:** System prompt for the AI. Contains {topic} placeholder.
**Image:** Wikimedia Commons portrait URL (or _Not available on Wikidata_)
**Voice Sample:** Wikimedia Commons audio URL (or _Not available on Wikidata_)
```

## Field Reference

| Field | Purpose | Source |
|-------|---------|--------|
| **Name** | Display name of the avatar | Manual |
| **Wikidata** | Link to Wikidata entity (QID) for structured metadata | Wikidata API |
| **Description** | Short personality tagline for UI display | Manual |
| **Prompt** | System prompt injected into the LLM. Use `{topic}` as the debate topic placeholder | Manual |
| **Image** | Portrait photo/image URL from Wikimedia Commons (property P18) | Wikidata |
| **Voice Sample** | Audio recording URL from Wikimedia Commons (property P990) | Wikidata |

## How to Use in an Application

### 1. Parse the avatars

Each avatar block is separated by `---`. Parse the markdown to extract fields per avatar.

### 2. Inject the debate topic

Replace `{topic}` in the **Prompt** field with the actual debate topic:

```python
prompt = avatar["prompt"].replace("{topic}", "universal basic income")
```

### 3. Use the image

The **Image** URLs point to Wikimedia Commons via `Special:FilePath/`, which redirects to the actual image file. These can be used directly in `<img>` tags or downloaded.

### 4. Use the voice sample

Voice samples (where available) are `.ogg`, `.wav`, `.mp3`, or `.flac` files hosted on Wikimedia Commons. These are real recordings of the person speaking and can be used as reference audio for voice cloning/TTS systems.

## Data Coverage

- **Images:** 44/47 avatars have Wikimedia Commons photos
- **Voice Samples:** 8/47 avatars have voice recordings on Wikidata
- **Missing images:** Hannibal Lecter, Freddy Krueger, Tyler Durden (fictional characters without free-license images)
- Avatars marked `_Not available on Wikidata_` need manual sourcing

## Wikidata Properties Used

| Property | Description |
|----------|-------------|
| P18 | Image (main portrait) |
| P990 | Audio recording of the subject's voice |
| P373 | Wikimedia Commons category |
| P935 | Wikimedia Commons gallery |

## Enrichment Process

Data was enriched by querying the [Wikidata API](https://www.wikidata.org/w/api.php):

1. Search for each persona name via `wbsearchentities`
2. Fetch entity claims via `wbgetentities`
3. Extract P18 (image) and P990 (voice) property values
4. Convert filenames to Wikimedia Commons `Special:FilePath/` URLs
5. For fictional characters, manual QID resolution was needed (Wikidata search often returns wrong entities for ambiguous names like "Batman", "Hulk", "Yoda")
