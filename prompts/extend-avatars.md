# Session Prompt: Extend AI Avatars List

Copy-paste this prompt at the start of a new Claude Code session in the `ai-avatars` project directory:

---

I'm working on the `ai-avatars` project. The file `avatars_debate.md` contains AI debate avatar personas enriched with Wikidata data.

I want to add new avatars to the list. For each new avatar:

1. **Write the entry** following the exact format in `CLAUDE.md` — Name, Wikidata QID, Description, Prompt (with `{topic}` placeholder and "1–2 sentences only" constraint), Image, Voice Sample.

2. **Enrich from Wikidata** — Query the Wikidata API (`wbsearchentities` then `wbgetentities`) to get:
   - **P18** (image) → convert to `https://commons.wikimedia.org/wiki/Special:FilePath/FILENAME` URL
   - **P990** (voice recording) → same URL format
   - Be careful with fictional/ambiguous names — verify the QID description matches the intended character before using it.

3. **Append** the new entries to the end of `avatars_debate.md` (before the final blank line), maintaining the `---` separator between entries.

Here are the new avatars I want to add:

- [LIST YOUR NEW NAMES HERE]

Please research Wikidata for each, write their entries, and append them to the file.

---

## Tips for choosing good avatars

Aim for diversity across these dimensions:
- **Era**: Ancient, historical, modern, contemporary
- **Domain**: Politics, arts, science, sports, entertainment, fiction
- **Style**: Aggressive, gentle, logical, emotional, humorous, cryptic
- **Gender/culture**: Global representation
- **Real vs fictional**: Mix of both

## Example names to consider

### Historical
- Nikola Tesla, Sun Tzu, Ada Lovelace, Genghis Khan, Socrates, Leonardo da Vinci, Napoleon Bonaparte, Marie Curie

### Modern public figures
- Oprah Winfrey, Barack Obama, Malala Yousafzai, Pope Francis, Jacinda Ardern, Volodymyr Zelenskyy

### Artists & musicians
- David Bowie, Amy Winehouse, Salvador Dali, Rihanna, Tupac Shakur, Lady Gaga, Freddie Mercury

### Fictional characters
- Darth Vader, Tony Stark, The Joker, Gandalf, Lara Croft, Morpheus, Tyrion Lannister, Captain Jack Sparrow

### Scientists & thinkers
- Albert Einstein, Noam Chomsky, Carl Sagan, Stephen Hawking, Nikola Tesla, Richard Feynman
