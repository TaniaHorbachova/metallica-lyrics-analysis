# Metallica Lyrics Analysis: Words Behind the Riffs

What does Metallica sing about? This project turns the lyrics of 141 songs into a word-frequency dataset, groups the words into 15 themes, and shows the results in an interactive Tableau dashboard.

![Dashboard preview](D:/DATAS/0.Tableau/HW5/Word Cloud/Metallica/dashboard.png)

**Live dashboard:** [Tableau Public](https://public.tableau.com/app/profile/tania.horbachova/viz/ThewordsofMetallica/Dashboard1?publish=yes)

## Key facts

| Metric | Value |
|---|---|
| Songs analysed | 141 |
| Unique words after cleaning | 2,252 |
| Word mentions after cleaning | 13,644 |
| Themed words shown in the dashboard | 615 (8,297 mentions) |
| Themes | 15 |

## Tools

| Purpose | Tools |
|---|---|
| Data loading | Python, pandas, kagglehub |
| Text processing | spaCy (lemmatization, part-of-speech filtering) |
| Export | openpyxl (Excel) |
| Visualization | Tableau Public |

## Method

1. **Load the data.** The dataset is downloaded from Kaggle with `kagglehub`. Each song has an album and the release date of its first appearance.
2. **Select songs.** Instrumentals, covers of other bands and duplicate songs were removed. 141 songs remained.
3. **Clean the text.**
   - The text was converted to lowercase and split into words.
   - Prepositions, conjunctions, particles, pronouns, interjections and other function words were removed, together with filler sounds such as "oh" and "yeah".
   - Only nouns, adjectives, verbs and adverbs with three or more letters were kept.
   - Different forms of the same word were merged (for example, *killed* and *kills* became *kill*).
4. **Count the words.** Each word was counted per song, so the final table has one row for every word and song.
5. **Assign themes.** Each word was assigned to a theme with a custom word list (`data/category_map.csv`) that was reviewed manually.
6. **Filter for the dashboard.** Words mentioned fewer than 3 times (`Rare words`) and general words without a clear theme (`Other`) are not shown in the charts.

### Themes

Life & Death, War & Violence, Emotions, Mind & Madness, Religion & Myth, Time, Nature, People & Body, Movement & Action, Freedom & Control, Society, Home & Places, Technology, Culture, Language.

Words that did not fit any theme are labeled `Other`. Words mentioned fewer than 3 times are labeled `Rare words (<3)`.

### How to read the numbers

Frequency counts every mention, including repeated lines in choruses. A word from a chorus can therefore look more common than the number of songs it appears in. The dashboard shows both numbers in the tooltip.

## Output

`data/metallica_words.xlsx` has one row for every word and song:

| Column | Description |
|---|---|
| Word | Lemmatized word |
| Frequency | Number of mentions in the song |
| Category | Theme of the word |
| Song Name | Song title |
| Album | Album of the first appearance |
| Release Year | Year of the album release |

## How to run

```bash
pip install pandas spacy openpyxl kagglehub
python -m spacy download en_core_web_sm
```

Open `notebook/metallica_lyrics_analysis.ipynb` and run the cells in order. The notebook downloads the dataset by itself and writes the final Excel file.

## Data source and notes

- Dataset: [Metallica Songs w/ Lyrics](https://www.kaggle.com/datasets/dmytroievdokymov/metallica-songs-w-lyrics) on Kaggle.
- The song lyrics belong to their rights holders and are **not** included in this repository. Only word counts and theme labels are shared.
- Theme assignment is subjective. Some words could belong to more than one theme.
- The code is released under the MIT License.

## Автор

Tania Horbachova 

Email: t.horbachova.data@gmail.com 

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?style=for-the-badge&logo=linkedin)](https://www.linkedin.com/in/tania-horbachova-8b5117115/)
