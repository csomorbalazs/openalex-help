# Get a single concept

It's easy to get a concept from from the API with: `/concepts/<entity_id>`. Here's an example:

* Get the concept with the [OpenAlex ID](./#the-openalex-id) `C71924100`:\
  [https://api.openalex.org/concepts/C71924100](https://api.openalex.org/concepts/C71924100)

That will return a [`Concept`](broken-reference) object, describing everything OpenAlex knows about the concept with that ID:

```json
{
    "id": "https://openalex.org/C71924100",
    "wikidata": "https://www.wikidata.org/wiki/Q11190",
    "display_name": "Medicine",
    "level": 0,
    "description": "field of study for diagnosing, treating and preventing disease",
    // other fields removed for brevity
}
```

{% hint style="info" %}
You can make up to 50 of these queries at once by [requesting a list of entities and filtering on IDs using OR syntax](broken-reference).
{% endhint %}

### External IDs

You can look up concepts using external IDs such as a wikidata ID:

* Get the concept with wikidata ID Q11190:\
  [https://api.openalex.org/concepts/wikidata:Q11190](https://api.openalex.org/concepts/wikidata:Q11190)

Available external IDs for concepts are:

| External ID                    | URN        |
| ------------------------------ | ---------- |
| Microsoft Academic Graph (MAG) | `mag`      |
| Wikidata                       | `wikidata` |

### Select fields

You can use `select` to limit the fields that are returned in a concept object. More details are [here](../get-lists-of-entities/select-fields.md).

* Display only the `id` and `display_name` for a concept object\
  [https://api.openalex.org/concepts/C71924100?select=id,display\_name](https://api.openalex.org/concepts/C71924100?select=id,display\_name)
