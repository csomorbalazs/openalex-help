---
description: People who create works
---

# 👩 Authors

## 👩 Authors

Authors are people who create works.

OpenAlex indexes about 213M authors, with thousands added daily. You can get an author from the API like this:

* Get the author with ORCID `https://orcid.org/0000-0002-1298-3089` [https://api.openalex.org/authors/https://orcid.org/0000-0002-1298-3089](https://api.openalex.org/authors/https://orcid.org/0000-0002-1298-3089)

The [Canonical External ID](broken-reference) for authors is ORCID; only a small percentage of authors have one, but the percentage is higher for more recent works.

Our information about authors comes from MAG, Crossref, PubMed, ORCID, and publisher websites. We use an algorithm to [disambiguate](https://en.wikipedia.org/wiki/Author\_name\_disambiguation) authors; this uses an author’s name, their publication record, their citation patterns, and (where available) their ORCID.

So for example, if J. Schmidt and John Jacob Jingleheimer Schmidt both write about 19th-century ketchup production, we’ll treat them as one author–but we won’t include the JJJ Schmidt who writes about weasel migration (even though his name is their name, too).

Authors are linked to works via the [`works.authorships`](https://github.com/ourresearch/openalex-docs/blob/sandbox/the-data/works/work-object/README.md#authorships) property.

MORE COMING SOON

## Limitations

### Works with more than 100 authors are truncated
