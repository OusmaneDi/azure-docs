---
title: Using Redis modules with Azure Cache for Redis
description: You can use Redis modules with your Azure Cache for Redis instances.
author: flang-msft

ms.author: franlanglois
ms.service: cache
ms.topic: conceptual
ms.date: 07/26/2022
ms.custom: template-concept

---
# Use Redis modules with Azure Cache for Redis

With Azure Cache for Redis, you can use Redis modules as libraries to add more data structures and functionality to the core Redis software. You add the modules at the time you're creating your Enterprise tier cache.

For more information on creating an Enterprise cache, see [Quickstart: Create a Redis Enterprise cache](quickstart-create-redis-enterprise.md).

Modules were introduced in open-source Redis 4.0. The modules extend the use-cases of Redis by adding functionality like search capabilities and data structures like **bloom and cuckoo filters**.

## Scope of Redis modules

Some popular modules are available for use in the Enterprise tier of Azure Cache for Redis:

| Module |Basic, Standard, and Premium  |Enterprise  |Enterprise Flash  |
|---------|---------|---------|---------|
|RediSearch   |    No   |    Yes     | Yes (preview)    |
|RedisBloom   |      No   |    Yes    |   No    |
|RedisTimeSeries |   No    |    Yes   |   No    |
|RedisJSON  |     No    |  Yes    |   Yes      |

Currently, `RediSearch` is the only module that can be used concurrently with active geo-replication.

> [!NOTE]
> Currently, you can't manually load any modules into Azure Cache for Redis. Manually updating modules version is also not possible.
>

## Client library support

The standard Redis client libraries have a varying amounts of support for each module. Some modules have specific libraries that add client support. Check the Redis [documentation pages](#modules) for each module to see more detail on which client libraries support them.

## Adding modules to your cache

You must add modules when you create your Enterprise tier cache. To add a module or modules when creating a new cache, use the settings in the Advanced tab of the Enterprise tier caches.

You can add all the available modules or to select only specific modules to install.

:::image type="content" source="media/cache-how-to-use-modules/cache-add-modules.png" alt-text="Screenshot of advanced tab showing a list of modules to add to a new cache. ":::

> [!IMPORTANT]
> Modules must be enabled at the time you create an Azure Cache for Redis instance.

For more information, see [Quickstart: Create a Redis Enterprise cache](quickstart-create-redis-enterprise.md).

## Modules

The following modules are available when creating a new Enterprise cache.

- [RediSearch](#redisearch)
- [RedisBloom](#redisbloom)
- [RedisTimeSeries](#redistimeseries)
- [RedisJSON](#redisjson)

### RediSearch

The **RediSearch** module adds a real-time search engine to your cache combining low latency performance with powerful search features.

Features include:

- Multi-field queries
- Aggregation
- Prefix, fuzzy, and phonetic-based searches
- Auto-complete suggestions
- Geo-filtering
- Boolean queries

Additionally, **RediSearch** can function as a secondary index, expanding your cache beyond a key-value structure and offering more sophisticated queries.

You can use **RediSearch** is used in a wide variety of use-cases, including real-time inventory, enterprise search, and in indexing external databases. [For more information, see the RediSearch documentation page](https://redis.io/docs/stack/search/).

>[!IMPORTANT]
> The RediSearch module can only be used with the `Enterprise` clustering policy. For more information, see [Clustering Policy](quickstart-create-redis-enterprise.md#clustering-policy).

>[!NOTE]
> The RediSearch module is the only module that can be used with active geo-replication.

### RedisBloom

RedisBloom adds four probabilistic data structures to a Redis server: **bloom filter**, **cuckoo filter**, **count-min sketch**, and **top-k**. Each of these data structures offers a way to sacrifice perfect accuracy in return for higher speed and better memory efficiency.

| **Data structure**   |  **Description**      |  **Example application**|
| ---------------------|------------------------|-------------------------|
| **Bloom and Cuckoo filters** | Tells you if an item is either (a) certainly not in a set or (b) potentially in a set.    |   Checking if an email has already been sent to a user|
|**Count-min sketch** | Determines the frequency of events in a stream | Counting how many times an IoT device reported a temperature under 0 degrees Celsius.  |
|**Top-k**   | Finds the `k` most frequently seen items |  Determine the most frequent words used in War and Peace. (for example, setting k = 50 will return the 50 most common words in the book) |

**Bloom and Cuckoo** filters are similar to each other, but each has a unique set of advantages and disadvantages that are beyond the scope of
this documentation.

For more information, see [RedisBloom](https://redis.io/docs/stack/bloom/).

### RedisTimeSeries

The **RedisTimeSeries** module adds high-throughput time series capabilities to your cache. This data structure is optimized for high volumes of incoming data and contains features to work with time series data, including:

- Aggregated queries (for example, average, maximum, standard deviation, etc.)
- Time-based queries (for example, start-time and end-time)
- Downsampling/decimation
- Data labeling for secondary indexing
- Configurable retention period

This module is useful for many applications that involve monitoring streaming data, such as IoT telemetry, application monitoring, and anomaly detection.

For more information, see [RedisTimeSeries](https://redis.io/docs/stack/timeseries/).

### RedisJSON

The **RedisJSON** module adds the capability to store, query, and search JSON-formatted data. This functionality is useful for storing document-like data within your cache.

Features include:

- Full support for the JSON standard
- Wide range of operations for all JSON data types, including objects, numbers, arrays, and strings
- Dedicated syntax and fast access to select and update elements inside documents

The **RedisJSON** module is also designed for use with the **RediSearch** module to provide integrated indexing and querying of data within a Redis server. Using both modules together can be a powerful tool to quickly retrieve specific data points within JSON objects.

Some common use-cases for **RedisJSON** include applications such as searching product catalogs, managing user profiles, and caching JSON-structured data.

For more information, see [RedisJSON](https://redis.io/docs/stack/json/).

## Next steps

- [Quickstart: Create a Redis Enterprise cache](quickstart-create-redis-enterprise.md)
- [Client libraries](cache-best-practices-client-libraries.md)
