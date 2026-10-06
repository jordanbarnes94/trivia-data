# trivia-data

Static, date-indexed datasets for scheduled trivia routines. Everything here is
prebuilt offline; a routine reads one small file per day and never scrapes
anything itself.

## Query contract

Every dataset follows the same layout:

    datasets/<dataset>/days/MM-DD.json   one file per calendar day
    datasets/<dataset>/all.json          every record, for ad-hoc queries
    datasets/<dataset>/SCHEMA.md         fields, sources, scope, build date, counts

Fetch today's file with:

    curl -sf https://raw.githubusercontent.com/jordanbarnes94/trivia-data/main/datasets/<dataset>/days/MM-DD.json

- `MM-DD` is zero-padded (`09-28`).
- All 366 day files always exist, including `02-29`. In a non-leap year, a
  routine running on 28 February should also read `02-29`.
- A day with nothing on it still has a file, with empty lists. **A 404 always
  means the fetch went wrong**, never a quiet day.

## Datasets

- [`curious-deaths`](datasets/curious-deaths/SCHEMA.md): people and events from
  Wikipedia's lists of last words, lists of unusual deaths and list of inventors
  killed by their own invention, up to the 20th century, with each person listed
  on their death day and on their birthday.

## How it is built

The build scripts and their fetch cache live in a separate private repository.
They are cached and incremental, so a rebuild re-fetches nothing it already
has. This repository holds only their output.

## Licence

The content is derived from Wikipedia (text, CC BY-SA 4.0) and Wikidata (CC0).
Reuse must credit Wikipedia and carry the same licence.
