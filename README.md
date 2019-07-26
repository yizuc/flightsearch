# Airline Ticket Retrieval Study

This repository contains the data used in the airline ticketing user
study, as described in the paper "[Item Retrieval As Utility
Estimation](https://ti.arc.nasa.gov/publications/52165/download/)".
Please refer to this paper for additional details on the data.

If you use this data in your publication, please include the following
citation:

    @inproceedings{Wolfe18itemretrieval,
     author = {Wolfe, Shawn R. and Zhang, Yi},
     title = {Item Retrieval As Utility Estimation},
     booktitle = {The 41st International ACM SIGIR Conference on Research and Development in Information Retrieval},
     year = {2018},
    } 


## [design](design) subdirectory
---

The design subdirectory contains the data needed to run the
experiment. It consists of two types of data:

  * [Topics](design/topics) subdirectory: Each file consists of a
    separate scenario that described the user need. This information
    was provided to the experimental subject to define the task.

  * [Tickets](design/tickets.csv): This file defines the scenario,
    ticket identifier (tid), and the nine numeric ticket
    attributes. These attributes were the only ticket information
    provided in the experiment. Only the tickets corresponding to the
    given scenario were available to be searched, essentially defining
    20 separate corpora.

## [responses](responses) subdirectory
---

The responses subdirectory contains all the user response data
(queries, search results, and tickets chosen).

  * [Queries](responses/queries.csv): this file contains the first
    query for every test subject (`worker`) and scenario pair. Not all
    search engines (`paradigm`) used all query input types: for
    instance, `SimpleMAUT` and `Tradeoff` did not use explicit orders, and
    `Lexical` and `SortedBoolean` did not use attribute
    importance. `SimpleMAUT` and `Tradeoff` took single attribute values
    as query input, but for format consistency, are recorded as a min
    and max of a single point. Ascending sort orders have '+'
    prepended; descending sort orders have '-' prepended.

  * Search results: Search results are given as
    [TREC](https://trec.nist.gov)-style runs, with results separated
    by search engine. Each line has the following format:
    `queryid iteration docid rank score run-name`, where:
    1. **queryid** is the query identifier.
    2. **iteration** is the query in the session. Only the first query is included, and as we use 0-numbering this is always 0.
    3. **docid** is the identifier of the ticket.
    4. **rank** is the rank of the ticket in the search results.
    5. **score** is the 'score' for ticket. We created a composite score of 'rank'.'score' to ensure the rank would be consistent in the case of ties. (Ties were broken by ticket identifier.) `SortedBoolean` and `Lexical` do not create scores during the ranking process.
    6. **run-name** is the search engine that produced the results.
    Docid `0` was used to indicate no results (a pseudo-result, as no
    ticket was given an identifier of 0).
  * [Relevance scores](responses/qrels.txt): The relevance score of the
    tickets are given as [TREC](https://trec.nist.gov)-style qrel
    files. Each line has the following format: `queryid iteration docid rel`,
    where:
    1. **queryid** is the query identifier.
    2. **iteration** is the query in the session. Only the first query is included, and as we use 0-numbering this is always 0.
    3. **docid** the identifier of the ticket.
    4. **rel** is the relevance status of the ticket, where 1 indicates the ticket was selected by the test subject.

## Errata
---

A cut-and-paste error led to an overweighting of the returning flight
duration for the `Tradeoff` paradigm. Returning flight duration was
rarely specified and the error had little effect on the results. The
rankings provided here correct for this error, and so retrieval
metrics for `Tradeoff` will differ slightly from the published
evaluation.
