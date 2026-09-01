# Open-Trivia Question Collections

This repo hosts **shareable category packs** for Open‑Trivia.

## How It Works
- Each category is packaged as a zip with:
  - `questions.csv`
  - optional `images/` folder
- The app can import a repo zip directly (or a per‑category zip).

Browse collections at `questions.trivia.gamedirection.net`.

## How To Contribute
1. **Fork** this repo to your GitHub account.
2. Add your category pack zip(s) to your fork.
3. Update the **Community Collections** list below with:
   - `Username`
   - `Categories`
   - `Question count`
   - Direct **zip link** to your repo (or per‑category zip)
4. Open a **pull request** back to this repo.

## Community Collections
Add your entry below:

| Username | Categories | Question Count | Zip Link |
| --- | --- | --- | --- |
| Template | Places | 1 | https://github.com/gamedirection/Open-Trivia-Questions/releases/download/latest/template-category.zip |
| [Uberspot](https://github.com/uberspot/OpenTriviaQA) | animals,brain-teasers,celebrities,entertainment,for-kids,general,geography,history,hobbies,humanities,literature,movies,music,newest,people,rated,religion-faith,science-technology,sports,television,video-games,world | 24 |  [OpenTriviaQA](https://github.com/uberspot/OpenTriviaQA) |
| [Gamedirection](https://github.com/Gamedirection) (live instance) | 44 categories, listed in [live/README.md](live/README.md) | 53394 | [live/category_archives/](live/category_archives/) |

The `live/` directory holds a generated snapshot of everything currently published
on the live Open-Trivia instance, as a combined CSV, a CSV per category, and an
importable zip per category. See [live/README.md](live/README.md).

OpenSource DB of trivia: [https://opentdb.com/](https://opentdb.com/)

## Notes
- Keep CSV headers aligned with the template.
- Only include images you have rights to use.
- Security warning: only import zips from trusted sources.
