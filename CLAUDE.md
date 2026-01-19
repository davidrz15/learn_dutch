# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Dutch vocabulary learning tool built with standalone HTML files. Each flashcard app is a self-contained HTML file with embedded CSS and JavaScript that works offline.

## Architecture

- **`index.html`** - Lesson selector that routes users to the appropriate flashcard file
- **`dutch-vocab-flashcards {DEEL}.{THEMA}.html`** - Individual flashcard apps (e.g., `1.1`, `1.2`, etc.)
- **`vocab-flashcards.skill`** - Skill file containing workflow instructions for generating new flashcard files
- **PDF files** - Source vocabulary lists from the Code+ Dutch course

## Using the vocab-flashcards Skill

When the user provides a new vocabulary PDF and wants to create flashcards:

1. **Extract the skill**: `unzip -o vocab-flashcards.skill -d /tmp/skill-extract`
2. **Read the instructions**: `/tmp/skill-extract/vocab-flashcards/SKILL.md`
3. **Use the template**: `/tmp/skill-extract/vocab-flashcards/assets/flashcard-template.html`

The skill defines a 7-step workflow:
1. Extract Deel/Thema numbers from PDF title
2. Extract vocabulary organized by sections (Intro, Taak 1-4, Slot)
3. Structure as JavaScript object
4. Generate HTML using the template
5. Add lesson identification (title, header, localStorage key)
6. Save as `dutch-vocab-flashcards {DEEL}.{THEMA}.html`
7. **Update `index.html`** to enable the new theme in both `availableLessons` object and the dropdown

## Key Patterns

- **localStorage keys**: `dutchLearnedWords_Deel{X}_Thema{Y}` - keeps progress separate per theme
- **Filename convention**: `dutch-vocab-flashcards {DEEL}.{THEMA}.html`
- **Sections in vocabulary**: Typically Intro, Taak 1, Taak 2, Taak 3, Taak 4, Slot (sometimes Lezen)

## When Adding New Themes

After creating a new flashcard HTML file, always update `index.html`:
1. Add entry to the `availableLessons` JavaScript object
2. Enable/add the option in `<select id="thema-select">`
3. If new Deel, also update `<select id="deel-select">`
