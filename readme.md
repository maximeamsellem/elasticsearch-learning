<!-- prettier-ignore-start -->

# Pre requisites

I got started here : https://www.elastic.co/guide/en/elasticsearch/reference/current/docker.html

I had to provide more than 4GB memory to docker engine.

Docker version: 18.03.1-ce,
Docker compose version:1.21.1

Others docs :

    - https://www.elastic.co/guide/en/elasticsearch/reference/current/getting-started-index.html

# ES wording

    - filters
    - analysers

# Search

    - filters does not affect the score but the presence of the document in the result.
    - ES uses analysers to change value during analysis (cf the example below)

    - [Range Query](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl-range-query.html)
    - [Match Query](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl-match-query.html)
    - [Synonyms graph token filter](https://www.elastic.co/guide/en/elasticsearch/reference/current/analysis-synonym-graph-tokenfilter.html)

## term vs match

avoid using term for text search.

Example:

    - you index a "text" property with value "Quick Brown Foxes!"
    - because the field is a "text" property es will will change "Quick Brown Foxes!" to [quick, brown, fox] duting analysis
    - therefore using : "term": { "full_text": "Quick Brown Foxes!" } - won't return a result - while : "match": { "full_text": "Quick Brown Foxes!" }

This is because the default standard analyzer changes text field values as follows:

    - Removes most punctuation
    - Divides the remaining content into individual words, called tokens
    - Lowercases the tokens

cf: https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl-term-query.html
