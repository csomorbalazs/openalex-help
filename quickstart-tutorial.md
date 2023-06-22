# Quickstart tutorial

## Quickstart tutorial

When you first visit openalex.org, you will see a search box where you can begin your exploration.

#### 1. Find the institution

You can use the [institutions](the-data/institutions.md) endpoint to learn about universities and research centers. OpenAlex has a powerful search feature that searches across 108,000 institutions.

Lets use it to search for Stanford University:

* Find Stanford University\
  [`https://api.openalex.org/institutions?search=stanford`](https://api.openalex.org/institutions?search=stanford)

Our first result looks correct (yeah!):

```json
{
  "id": "https://openalex.org/I97018004",
  "ror": "https://ror.org/00f54p054",
  "display_name": "Stanford University",
  "country_code": "US",
  "type": "education",
  "homepage_url": "http://www.stanford.edu/"
  // other fields removed
}
```

We can use the ID `https://openalex.org/I97018004` in that result to find out more.

#### 2. Find articles (works) associated with Stanford University

The [works](the-data/works/) endpoint contains over 240 million articles, books, and theses :astonished:. We can filter to show works associated with Stanford.

* Show works where at least one author is associated with Stanford University\
  [`https://api.openalex.org/works?filter=institutions.id:https://openalex.org/I97018004`](https://api.openalex.org/works?filter=institutions.id:https://openalex.org/I97018004)

This is just one of the 50+ ways that you can filter works!

#### 3. Filter works by publication year

Right now the list shows records for all years. Lets narrow it down to works that were published between 2010 to 2020, and sort from newest to oldest.

* Show works with publication years 2010 to 2020, associated with Stanford University\
  [https://api.openalex.org/works?filter=institutions.id:https://openalex.org/I97018004,publication\_year:2010-2020\&sort=publication\_date:desc](https://api.openalex.org/works?filter=institutions.id:https://openalex.org/I97018004,publication\_year:2010-2020\&sort=publication\_date:desc)

#### 4. Group works by publication year to show counts by year

Finally, you can group our result by publication year to get our final result, which is the number of articles produced by Stanford, by year from 2010 to 2020. There are more than 30 ways to group records in OpenAlex, including by publisher, journal, and open access status.

* Group records by publication year\
  [`https://api.openalex.org/works?filter=institutions.id:https://openalex.org/I97018004,publication\_year:2010-2020\&group-by=publication\_year`](https://api.openalex.org/works?filter=institutions.id:https://openalex.org/I97018004,publication\_year:2010-2020\&group-by=publication\_year)

That gives a result like this:

```json
[
  {
    "key": "2020",
    "key_display_name": "2020",
    "count": 18627
  },
  {
    "key": "2019",
    "key_display_name": "2019",
    "count": 15933
  },
  {
    "key": "2017",
    "key_display_name": "2017",
    "count": 14789
  },
  ...
]
```

There you have it! This same technique can be applied to hundreds of questions around scholarly data. The data you received is under a [CC0 license](https://creativecommons.org/publicdomain/zero/1.0/), so not only did you access it easily, you can share it freely! :tada:

### What's next?

Jump into an area of OpenAlex that interests you:

* [Works](the-data/works/)
* [Authors](the-data/authors/)
* [Sources](the-data/sources.md)
* [Institutions](the-data/institutions.md)
* [Concepts](the-data/concepts.md)
* [Publishers](the-data/publishers.md)
* [Funders](the-data/funders.md)

And check out our [tutorials](additional-help/tutorials.md) page for some hands-on examples!
