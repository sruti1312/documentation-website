---
layout: default
title: About ML Commons
nav_order: 1
has_children: false
has_toc: false
---

# ML Commons plugin

ML Commons for OpenSearch eases the development of machine learning features by providing a set of common machine learning (ML) algorithms through transport and REST API calls. Those calls choose the right nodes and resources for each ML request and monitors ML tasks to ensure uptime. This allows you to leverage existing open-source ML algorithms and reduce the effort required to develop new ML features.

Interaction with the ML commons plugin occurs through either the [REST API]({{site.url}}{{site.baseurl}}/ml-commons-plugin/api) or [AD]({{site.url}}{{site.baseurl}}/observability-plugin/ppl/commands#ad) and [kmeans]({{site.url}}{{site.baseurl}}/observability-plugin/ppl/commands#kmeans) PPL commands.

Models [trained]({{site.url}}{{site.baseurl}}/ml-commons-plugin/api#train-model) through the ML Commons plugin support model-based algorithms such as kmeans. After you've trained a model enough so that it meets your precision requirements, you can apply the model to [predict]({{site.url}}{{site.baseurl}}/ml-commons-plugin/api#predict) new data safely. 

Should you not want to use a model, you can use the [Train and Predict]({{site.url}}{{site.baseurl}}/ml-commons-plugin/api#train-and-predict) API to test your model without having to evaluate the model's performance.


## Permissions

There are two reserved user roles that can use of the ML commons plugin.

- `ml_full_access`: Full access to all ML features, including starting new ML tasks and reading or deleting models.
- `ml_readonly_access`: Can only read ML tasks, trained models and statistics relevant to the model's cluster. Cannot start nor delete ML tasks or models.
