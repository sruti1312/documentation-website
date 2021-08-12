---
layout: default
title: Delete by query
parent: Document APIs
grand_parent: REST API reference
nav_order: 25
---

# Delete by query
Introduced 1.0
{: .label .label-purple}

You can include a query as part of your delete request so OpenSearch deletes all documents that match that query.

## Example

```json
POST sample-index1/_delete_by_query
{
  "query": {
    "match": {
      "movie-length": "124"
    }
  }
}
```

## Path and HTTP methods

```
POST <target>/_delete_by_query
```

## URL parameters

All URL parameters are optional.

Parameter | Type | Description
:--- | :--- | :--- | :---
&lt;index&gt; | String | Name of the data streams, indices, or aliases to delete from. Supports wildcards. If left blank, OpenSearch searches all indices.
allow_no_indices | Boolean | False indicates to OpenSearch the request should return an error if any wildcard expression or index alias targets only missing or closed indices. Default is true.
analyzer | String | The analyzer to use in the query string.
analyze_wildcard | Boolean | Specifies whether to analyze wildcard and prefix queries. Default is false.
conflicts | String | Indicates to OpenSearch what should happen if the delete by query operation runs into a version conflict. Valid options are `abort` and `proceed`. Default is `abort`.
default_operator | String | Indicates whether the default operator for a string query should be AND or OR. Default is OR.
df | String | The default field in case a field prefix is not provided in the query string.
expand_wildcards | String | Specifies the type of index that wildcard expressions can match. Supports comma-separated values. Valid values are `all` (match any index), `open` (match open, non-hidden indices), `closed` (match closed, non-hidden indices), `hidden` (match hidden indices), and `none` (deny wildcard expressions). Default is `open`.
from | Integer | The starting index to search from. Default is 0.
ignore_unavailable | Boolean | Specifies whether to include missing or closed indices in the response. Default is false.
lenient | Boolean | Specifies whether OpenSearch should ignore format-based query failures (for example, querying a text field for an integer). Default is false.
max_docs | Integer | Maximum amount of documents the operation should process. Default is all documents.
preference | String | Specifies the shard or node OpenSearch should perform the operation on.
q | String | Query in the Lucene query string syntax.
request_cache | Boolean | Specifies whether OpenSearch should use the request cache for the request. Default is whether it's enabled in the index's settings.
refresh | Boolean | Specifies whether OpenSearch should refresh all of the shards involved in the delete request once the operation finishes. Default is false.
requests_per_second | Integer | Specifies the request's throttling in sub-requests per second. Default is -1, which means no throttling.
routing | String | Value used to route the operation to a specific shard.
scroll | Time | Amount of time the search context should be open.
scroll_size | Integer | Size of the scroll request of the operation. Default is 1000.
search_type | String | Whether OpenSearch should use global term and document frequencies calculating revelance scores. Valid choices are `query_then_fetch` and `dfs_query_then_fetch`. `query_then_fetch` scores documents using local term and document frequencies for the shard. It’s usually faster but less accurate. `dfs_query_then_fetch` scores documents using global term and document frequencies across all shards. It’s usually slower but more accurate. Default is `query_then_fetch`.
search_timeout | Time | Amount of time until timeout for the search request. Default is no timeout.
slices | Integer | Number of sub-tasks OpenSearch should divide this task into. Default is 1, which means OpenSearch should not divide this task.
sort | String | A comma-separated list of &lt;field&gt; : &lt;direction&gt; pairs to sort by.
_source | String | Specifies whether to include the `_source` field in the response.
_source_excludes | String | A comma-separated list of source fields to exclude from the response.
_source_includes | String | A comma-separated list of source fields to include in the response.
stats | String | Value to associate with the request for additional logging.
terminate_after | Integer | The maximum number of documents OpenSearch should process before terminating the request.
timeout | Time | How long the operation should wait from a response from active shards. Default is `1m`.
version | Boolean | Whether to include the document version as a match.
wait_for_active_shards | String | The number of shards that must be active before OpenSearch executes the operation. Valid values are `all` or any integer up to the total number of shards in the index. Default is 1, which is the primary shard.

## Request body

To search your index for specific documents, you must include a [query]({{site.url}}{{site.baseurl}}/opensearch/query-dsl/index) in the request body that OpenSearch uses to match documents. If you don't use a query, OpenSearch treats your delete request as a simple [delete document operation]({{site.url}}{{site.baseurl}}/opensearch/rest-api/document-apis/delete-document).

```json
{
  "query": {
    "match": {
      "movie-length": "124"
    }
  }
}
```

## Response
```json
{
  "took": 143,
  "timed_out": false,
  "total": 1,
  "deleted": 1,
  "batches": 1,
  "version_conflicts": 0,
  "noops": 0,
  "retries": {
    "bulk": 0,
    "search": 0
  },
  "throttled_millis": 0,
  "requests_per_second": -1.0,
  "throttled_until_millis": 0,
  "failures": []
}
```

## Response body fields

Field | Description
:--- | :---
took | The amount of time in milliseconds OpenSearch needed to complete the operation.
timed_out | Whether any delete requests during the operation timed out.
total | Total number of documents processed.
deleted | Total number of documents deleted.
batches | Number of scroll responses the request processed.
version_conflicts | Number of conflicts the request ran into.
noops | How many delete requests OpenSearch ignored during the operation. This field always returns 0.
retries | The number of bulk and search retry requests.
throttled_millis | Number of throttled milliseconds during the request.
requests_per_second | Number of requests executed per second during the operation.
throttled_until_millis | The amount of time until OpenSearch executes the next throttled request. Always equal to 0 in a delete by query request.
failures | Any failures that occur during the request.