# 4. Monitor, troubleshoot, and optimize Azure solutions (15-20%)
## 4.1 Integrate caching and content delivery within solutions
### configure cache and expiration policies
- Caching rules are available only for **Azure CDN Standard from Verizon** and **Azure CDN Standard from Akamai** profiles
- 2 ways to control how files are cached:
    1. **Caching rules**
        - set or modify default cache expiration behavior both globally and with custom conditions (e.g.: URL path and file extension)
            - **Global caching rules**
            - **Custom caching rules**
    2. **Query string caching**: adjust how the Azure CDN treats caching for requests with query strings
- Caching behavior settings
    - **Bypass cache**: Do not cache and ignore origin-provided cache-directive headers.
    - **Override**: Ignore origin-provided cache duration; use the provided cache duration instead. This will not override cache-control: no-cache.
    - **Set if missing**: Honor origin-provided cache-directive headers, if they exist; otherwise, use the provided cache duration.
- Cache expiration duration
    - specify the cache expiration duration in days, hours, minutes, and seconds
        - **Override** and **Set if missing Caching behavior**:  valid cache durations range between 0 seconds and 366 days
            - for a value of 0 seconds, the CDN caches the content, but must revalidate each request with the origin server
        - **Bypass cache**: cache duration is automatically set to 0 seconds and cannot be changed
- Custom caching rules match conditions
    - **Path**: condition matches the path of the URL, excluding the domain name, and supports the wildcard symbol (*)
        - e.g.: /myfile.html, /my/folder/*, and /my/images/*.jpg.
    - **Extension**: condition matches the file extension of the requested file, provide a list of comma-separated file extensions to match
        - e.g.: , .jpg, .mp3, .png
- Set Azure CDN caching rules
    - Open the Azure CDN caching rules page
        - Azure Portal > CDN profile > select endpoint
        - Settings > Caching rules
    - Set global/custom caching rules

### configure cache and expiration policies for Azure Redis Cache
- Azure Portal >  Azure Cache for Redis
    - configure the eviction policy of the cache
### implement secure and optimized application cache patterns including data sizing, connections, encryption, and expiration
- Caching is most effective when a client instance repeatedly reads the same data, especially if all the following conditions apply to the original data store:
    - It remains relatively static.
    - It's slow compared to the speed of the cache.
    - It's subject to a high level of contention.
    - It's far away when network latency can cause access to be slow.
- **Cache-Aside Cloud Design Pattern**
    - ![](img/cache-aside-diagram.png)
- Caching in distributed applications
    - Private caching
        - ![](img/private-caching.png)
    - Shared caching
        - ![](img/shared-caching.png)
- Considerations 
    - Decide when to cache data
        - consider caching data that is read frequently but modified infrequently
        - less useful for dynamic data
        - used to avoid repeating computations while the application is running
    - Determine how to cache data effectively
        - analysis of usage patterns can help you decide whether to fully or partially prepopulate a cache
    - Cache highly dynamic data
        - cached information will nearly always be outdated
        - consider the benefits of storing the dynamic information directly in the cache instead of in the persistent data store
            - only if the data is noncritical and does not require auditing
    - Manage data expiration in a cache
        - configure the cache to expire data and reduce the period for which data may be out of date
        - eviction policies
            - A **most-recently-used policy** (in the expectation that the data will not be required again).
            - A **first-in-first-out policy** (oldest data is evicted first).
            - An **explicit removal policy** based on a triggered event (such as the data being modified)
    - Invalidate data in a client-side cache
        - if the expiration policies of the cache aren't properly implemented, a client might use outdated information that's cached locally when the information in the original data source has changed.
    - Managing concurrency in a cache: two approaches
        - **Optimistic**: Immediately prior to updating the data, the application checks to see whether the data in the cache has changed since it was retrieved. If the data is still the same, the change can be made. Otherwise, the application has to decide whether to update it. 
        - **Pessimistic**: When it retrieves the data, the application locks it in the cache to prevent another instance from changing it. This process ensures that collisions cannot occur, but they can also block other instances that need to process the same data.
    - Implement high availability and scalability, and improve performance
        - Using a local private cache in combination with a shared cache:
            - ![](img/ha-caching.png)
    - Caching and eventual consistency
        - One instance of an application could modify a data item and invalidate the cached version of that item. Another instance of the application might attempt to read this item from a cache, which causes a cache-miss, so it reads the data from the data store and adds it to the cache. However, if the data store has not been fully synchronized with the other replicas, the application instance could read and populate the cache with the old value.
    - Protect cached data
        - implement an authentication mechanism that requires that applications specify the following:
            - Which identities can access data in the cache.
            - Which operations (read and write) that these identities are allowed to perform.
        - restrict access to subsets of the cached data
            - Split the cache into partitions (by using different cache servers) and only grant access to identities for the partitions that they should be allowed to use.
            - Encrypt the data in each subset by using different keys, and provide the encryption keys only to identities that should have access to each subset. A client application might still be able to retrieve all of the data in the cache, but it will only be able to decrypt the data for which it has the keys.

## 4.2 Instrument solutions to support monitoring and logging
### configure an app or service to use Application Insights
[docs](https://docs.microsoft.com/en-us/azure/azure-monitor/app/azure-web-apps?tabs=netcore)

### analyze and troubleshoot solutions by using Azure Monitor
[docs](https://docs.microsoft.com/en-us/azure/app-service/tutorial-troubleshoot-monitor)

### implement Application Insights web tests and alerts
[docs](https://azure.microsoft.com/en-us/blog/creating-a-web-test-alert-programmatically-with-application-insights/)

e.g.: [Monitor availability with URL ping tests
](https://docs.microsoft.com/en-us/azure/azure-monitor/app/monitor-web-app-availability)