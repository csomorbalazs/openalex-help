---
description: Topics assigned to works
---

# 💡 Concepts

## 💡 Concepts

Concepts are abstract ideas that works are about.

OpenAlex indexes about 65k concepts. You can get a concept from the OpenAlex API like this:

* Get the concept with OpenAlex ID `C41008148`\
  [https://api.openalex.org/concepts/C41008148](https://api.openalex.org/concepts/C41008148)

The [Canonical External ID](../the-api/get-single-entities/#canonical-external-ids) for OpenAlex concepts is the Wikidata ID, and each of our concepts has one, because all OpenAlex concepts are also Wikidata concepts.

Concepts are hierarchical, like a tree. There are 19 root-level concepts, and six layers of descendants branching out from them, containing about 65 thousand concepts all told. This concept tree is a modified version of [the one created by MAG](https://arxiv.org/abs/1805.12216). You can view all the concepts and their position in the tree [as a spreadsheet here](https://docs.google.com/spreadsheets/d/1LBFHjPt4rj\_9r0t0TTAlT68NwOtNH8Z21lBMsJDMoZg/edit#gid=1473310811). About 85% of works are tagged with at least one concept (here's the [breakdown of concept counts per work](https://docs.google.com/spreadsheets/d/17DoJjyl1XVNZdVWs7fUy91z69U2tD8qtnBsaqJ-Zigo/edit#gid=0)).

### How concepts are assigned

Each work is tagged with multiple concepts, based on the title, abstract, and the title of its host venue. The tagging is done using an automated classifier that was trained on MAG’s corpus; you can read more about the development and operation of this classifier in [Automated concept tagging for OpenAlex, an open index of scholarly articles.](https://docs.google.com/document/d/1OgXSLriHO3Ekz0OYoaoP\_h0sPcuvV4EqX7VgLLblKe4/edit) You can implement the classifier yourself using [our models and code](https://github.com/ourresearch/openalex-concept-tagging).

A score is available for each [concept in a work](https://github.com/ourresearch/openalex-docs/blob/sandbox/the-data/works/work-object/README.md#concepts), showing the classifier's confidence in choosing that concept. However, when assigning a lower-level child concept, we also assign all of its parent concepts all the way up to the root. This means that some concept assignment scores will be 0.0. The tagger adds concepts to works written in different languages, but it is optimized for English.

Concepts are linked to works via the [`concepts`](https://github.com/ourresearch/openalex-docs/blob/sandbox/the-data/works/work-object/README.md#concepts) property. They’re also linked to [authors](https://github.com/ourresearch/openalex-docs/blob/sandbox/the-data/authors/author-object.md), [sources](https://github.com/ourresearch/openalex-docs/blob/sandbox/api-entities/sources/sources-object.md), and [institutions](https://github.com/ourresearch/openalex-docs/blob/sandbox/the-data/institutions/institution-object.md) via the `x_concepts` property, and to other concepts via the [`ancestors`](concepts.md#ancestors) and [`related_concepts`](concepts.md#related\_concepts) properties.

## Concept attributes

### `ancestors`

List of concepts that this concept descends from.

Ancestor concepts are represented as [dehydrated Concept](https://github.com/ourresearch/openalex-docs/blob/sandbox/the-data/concepts/concept-object.md#the-dehydratedconcept-object) objects. See the [concept tree section](https://github.com/ourresearch/openalex-docs/blob/sandbox/the-data/concepts/concept-object.md#the-concept-tree) for more details on how the different layers of concepts work together.

```json
ancestors: [
    {
        id: "https://openalex.org/C2522767166",
        wikidata: "https://www.wikidata.org/wiki/Q2374463",
        display_name: "Data science",
        level: 1
    },
    {
        id: "https://openalex.org/C161191863",
        wikidata: "https://www.wikidata.org/wiki/Q199655",
        display_name: "Library science",
        level: 1
    },
    
    // and so forth
]
```

### `cited_by_count`

The number of citations to works that have been tagged with this concept.

Less formally: the number of citations to this concept. For example, if there are just two works tagged with this concept and one of them has been cited 10 times, and the other has been cited 1 time, `cited_by_count` for this concept would be `11`.

```json
cited_by_count: 20248 
```

### `counts_by_year`

The works count and cited-by count of this concept for the last ten years, binned by year.

To put it another way: for every listed year, you can see how many new works were tagged with this concept, and how many times _any_ work tagged with this concept got cited.

Years with zero citations and zero works have been removed so you will need to add those back in if you need them.

```json
counts_by_year: [
    {
        year: 2021,
        works_count: 4211,
        cited_by_count: 120939
    },
    {
        year: 2020,
        works_count: 4363,
        cited_by_count: 119531
    },
    
    // and so forth
]
```

### `created_date`

The date this concept was created in the OpenAlex dataset.

Expressed as an [ISO 8601](https://en.wikipedia.org/wiki/ISO\_8601) date string.

```json
created_date: "2017-08-08"
```

### `description`

A brief description of this concept.

```json
description: "study of alternative metrics for analyzing and informing scholarship"
```

### `display_name`

The English-language label of the concept.

```json
display_name: "Altmetrics"
```

### `id`

The OpenAlex ID for this concept.

```json
id: "https://openalex.org/C2778407487"
```

### `ids`

All the external identifiers that we know about for this concept.

IDs are expressed as URIs whenever possible. Possible ID types:

* `mag` (_Integer:_ this concept's [Microsoft Academic Graph](https://www.microsoft.com/en-us/research/project/microsoft-academic-graph/) ID)
* `openalex` (_String:_ this concept's [OpenAlex ID](../the-api/get-single-entities/#the-openalex-id). Same as [`Concept.id`](https://github.com/ourresearch/openalex-docs/blob/sandbox/the-data/concepts/concept-object.md#id))
* `umls_cui` (_List:_ this concept's [Unified Medical Language System](https://www.nlm.nih.gov/research/umls/index.html) [Concept Unique Identifiers](https://www.nlm.nih.gov/research/umls/new\_users/online\_learning/Meta\_005.html))
* `umls_aui` (_List:_ this concept's [Unified Medical Language System](https://www.nlm.nih.gov/research/umls/index.html) [Atom Unique Identifiers](https://www.nlm.nih.gov/research/umls/new\_users/online\_learning/Meta\_005.html))
* `wikidata` (_String:_ this concept's [Wikidata ID](https://www.wikidata.org/wiki/Wikidata:Identifiers). Same as [`Concept.wikidata`](https://github.com/ourresearch/openalex-docs/blob/sandbox/the-data/concepts/concept-object.md#wikidata))
* `wikipedia` (_String:_ this concept's Wikipedia page URL)

{% hint style="info" %}
Many concepts are missing one or more ID types (either because we don't know the ID, or because it was never assigned). Keys for null IDs are not displayed..
{% endhint %}

```json
ids: {
    openalex: "https://openalex.org/C2778407487",
    wikidata: "https://www.wikidata.org/wiki/Q14565201",
    wikipedia: "https://en.wikipedia.org/wiki/Altmetrics",
    mag: 2778407487114027177
}
```

### `image_thumbnail_url`

URL where you can get a thumbnail image representing this concept.

```json
image_thumbnail_url: "https://upload.wikimedia.org/wikipedia/commons/thumb/f/f1/Altmetrics.svg/100px-Altmetrics.svg.png"
```

### `image_url`

URL where you can get an image representing this concept, where available.

Usually this is hosted on Wikipedia.

```json
image_url: "https://upload.wikimedia.org/wikipedia/commons/f/f1/Altmetrics.svg"
```

### `international`

This concept's display name in many languages, derived from article titles on each language's wikipedia.

See the [Wikidata entry](https://www.wikidata.org/wiki/Q137496#sitelinks-wikipedia) for "Java Bytecode" for example source data.

* `display_name` (_Object_)
  * `key` (String): language code in [wikidata language code](https://www.wikidata.org/wiki/Property:P9753) format. Full list of languages is [here](https://doc.wikimedia.org/mediawiki-core/master/php/Names\_8php\_source.html).
  * `value` (String): `display_name` in the given language

```json
international: {
    display_name: {
        ca: "Altmetrics",
        ...
    }
}
```

### `level`

The level in the concept tree where this concept lives, from 0 (most general) to 5 (most specific).

Lower-level concepts are more general, and higher-level concepts are more specific. [Computer Science](https://openalex.org/C41008148) has a level of 0; [Java Bytecode](https://openalex.org/C2777472213) has a level of 5. Level 0 concepts have no ancestors and level 5 concepts have no descendants.

```json
level: 2
```

### `related_concepts`

Concepts that are similar to this one.

Each listed concept is a [dehydrated Concept](https://github.com/ourresearch/openalex-docs/blob/sandbox/the-data/concepts/concept-object.md#the-dehydratedconcept-object) object, with one additional attribute:

* `score` (_Float_): The strength of association between this concept and the listed concept, on a scale of 0-100.

```json
related_concepts: [
    {
        id: "https://openalex.org/C2778793908",
        wikidata: null,
        display_name: "Citation impact",
        level: 3,
        score: 4.56749
    },
    {
        id: "https://openalex.org/C2779455604",
        wikidata: null,
        display_name: "Impact factor",
        level: 2,
        score: 4.46396
    }
    
    // and so forth
]
```

### `summary_stats`

Citation metrics for this concept

* `2yr_mean_citedness` _Float_: The 2-year mean citedness for this concept. Also known as [impact factor](https://en.wikipedia.org/wiki/Impact\_factor).
* `h_index` _Integer_: The [_h_-index](https://en.wikipedia.org/wiki/H-index) for this concept.
* `i10_index` _Integer_: The [i-10 index](https://en.wikipedia.org/wiki/Author-level\_metrics#i-10-index) for this concept.

While the _h_-index and the i-10 index are normally author-level metrics and the 2-year mean citedness is normally a journal-level metric, they can be calculated for any set of papers, so we include them for concepts.

```json
summary_stats: {
    2yr_mean_citedness: 1.5295340589458237,
    h_index: 105,
    i10_index: 5045
}
```

### `updated_date`

The last time anything in this concept's data changed (any change at all, including increases in various counts).

Expressed as an [ISO 8601](https://en.wikipedia.org/wiki/ISO\_8601) date string.

```json
updated_date: "2021-12-25T14:04:30.578837"
```

### `wikidata`

The Wikidata ID for this concept.

This is the [Canonical External ID](../the-api/get-single-entities/#canonical-external-ids) for concepts.

{% hint style="info" %}
_All_ OpenAlex concepts have a Wikidata ID, because all OpenAlex concepts are also Wikidata concepts.
{% endhint %}

```json
wikidata: "https://www.wikidata.org/wiki/Q14565201"
```

### `works_api_url`

A URL that will get you a list of all the works tagged with this concept via the OpenAlex API.

We express this as an API URL (instead of just listing the works themselves) because there might be millions of works tagged with this concept, and that's too many to fit here.

```json
works_api_url: "https://api.openalex.org/works?filter=concept.id:C2778407487"
```

### `works_count`

The number of works tagged with this concept.

```json
works_count: 3078 
```

## The `DehydratedConcept` object

The `DehydratedConcept` is stripped-down [`Concept`](https://github.com/ourresearch/openalex-docs/blob/sandbox/the-data/concepts/concept-object.md#the-concept-object) object, with most of its properties removed to save weight. Its only remaining properties are:

* ``[`display_name`](concept-object.md#display\_name)``
* ``[`id`](concept-object.md#id)``
* ``[`level`](concept-object.md#level)``
* ``[`wikidata`](concept-object.md#wikidata)``

## What's next

Using the API, you can fetch, filter, search, and group data about concepts:

* [Get a single concept](https://github.com/ourresearch/openalex-docs/blob/sandbox/the-data/concepts/get-a-single-concept.md)
* [Get lists of concepts](https://github.com/ourresearch/openalex-docs/blob/sandbox/the-data/concepts/get-lists-of-concepts.md)
* [Filter concepts](../the-api/filters/filter-concepts.md)
* [Search concepts](https://github.com/ourresearch/openalex-docs/blob/sandbox/the-data/concepts/search-concepts.md)
* [Group concepts](https://github.com/ourresearch/openalex-docs/blob/sandbox/the-data/concepts/group-concepts.md)
