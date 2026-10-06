# curious-deaths

People and events from Wikipedia's lists of last words, lists of unusual
deaths and list of inventors killed by their own invention, indexed by calendar day, covering up to and including the 20th century. Built 2026-10-06 from the pages below, with birth
dates from Wikidata (P569). Text is CC BY-SA 4.0, derived from Wikipedia.

## Query

    https://raw.githubusercontent.com/jordanbarnes94/trivia-data/main/datasets/curious-deaths/days/MM-DD.json

All 366 files exist, including 02-29. Empty `died` and `born` lists mean a quiet
day; a 404 means the fetch went wrong.

## Day file

- `date`: "MM-DD".
- `died`: entries whose date falls on this day, sorted by `year`. Usually that
  is the death; see `date_kind`.
- `born`: individuals born on this day who appear on the lists for their death,
  sorted by `year`. Someone born and died on the same calendar day appears in
  `died` only.

## Entry fields

- `year` (int, negative = BC) and `year_label` ("1805", "44 BC"): the year of
  the dated event for `died` entries, of the birth for `born` entries.
- `date_kind`: `death`, or `last_words` when the list dates the last words and
  the death came more than a year later (a coma, a disappearance). Such entries
  sit on the day of the last words; `died` gives the real death date.
- `tags`: display tags for the entry, in order: "Birth" (only in `born`
  entries), then "Unusual Death" and/or "Famous Last Words" by which list the
  entry comes from. Someone on both lists carries both. Entries from the list
  of inventors killed by their own invention carry "Unusual Death".
- `name`: as the list gives it.
- `kind`: `individual`, or `group` for an event with several victims
  (e.g. "Victims of the Great Molasses Flood"). Groups appear only in `died`.
- `desc`: one-line description from the last-words list, or null.
- `cause`: the circumstances of death as the list describes them, or null.
- `last_words`: the recorded last words, or null.
- `wikipedia`: the person's (or event's) article, or null.
- `born` (in `died` entries): the birth date, or null. Usually "D Month YYYY";
  where Wikidata knows only the month or the year it is "Month YYYY" or "YYYY",
  prefixed "c. " when Wikidata marks it approximate ("c. 1494"). Only a full
  date puts the person in a `born` list.
- `died`: the death date, as "D Month YYYY". In a `died` entry it differs from
  the file's day only when `date_kind` is `last_words`.

Dates are as Wikipedia and Wikidata state them, with no calendar conversion;
pre-1752 English and other pre-reform dates may be Julian. Where a list gives
only a year or a century, the day was recovered from Wikidata or the article's
opening text when it agreed with the list's year; `all.json` records which
source each date came from (`date_source`, `born_source`).

`all.json` is the source of truth: the day files are generated from it, and
the build fails unless every day file regenerates from it exactly. In
`all.json` a `born` known only to the month or year omits `d` (and `m`), and
carries `"circa": true` when approximate.

## Counts

- 1919 records (27 groups, 43 with a date recovered from Wikidata or the article)
- 1919 death-day entries, 1547 birthday entries
- 366 of 366 days have at least one entry

## Sources

- https://en.wikipedia.org/wiki/List_of_last_words
- https://en.wikipedia.org/wiki/List_of_last_words_(18th_century)
- https://en.wikipedia.org/wiki/List_of_last_words_(19th_century)
- https://en.wikipedia.org/wiki/List_of_last_words_(20th_century)
- https://en.wikipedia.org/wiki/List_of_unusual_deaths_in_antiquity
- https://en.wikipedia.org/wiki/List_of_unusual_deaths_in_the_Middle_Ages
- https://en.wikipedia.org/wiki/List_of_unusual_deaths_in_the_Renaissance
- https://en.wikipedia.org/wiki/List_of_unusual_deaths_in_the_early_modern_period
- https://en.wikipedia.org/wiki/List_of_unusual_deaths_in_the_19th_century
- https://en.wikipedia.org/wiki/List_of_unusual_deaths_in_the_20th_century
- https://en.wikipedia.org/wiki/List_of_inventors_killed_by_their_own_invention
