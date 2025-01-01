Caches are anything that helps you avoid expensive disk i/o or network i/o or computation

- An in-memory cache like Redis stores it in the RAM in a key value fashion but cache can be stored anywhere where an expensive i/o or network i/o is avoided.
- You typical check you logs and figure which endpoints are being accessed most frequently and cache them to decrease the database calls
- Example: Google News: Cache the Most recent released news since they are the ones that are most likely to be accessed
- We can Cache **Auth Tokens** since they are checked frequently and we need to check auth tokens for validity

### Ways to populate a Cache

## lazy Caching

The flow here is first API checks the cache for the key if it is expired or not available it will make an database call and populate cache along and return the content to the user

Writes are only done to database

```jsx
function getFromCache(key) {
    if (cache.has(key)) {
        return cache.get(key); // Cache hit
    } else {
        const value = fetchFromSource(key); // Fetch from source
        cache.set(key, value); // Populate cache
        return value;
    }
}
```

example: Blog caching

## Eager Caching

Eager caching preloads data into the cache, often at startup or based on predictions about usage patterns. It is proactive and aims to ensure that data is available in the cache before it's requested.

### **Advantages**:

1. **Low Latency**: Reduces or eliminates delays for the first request.
2. **Predictable Performance**: Applications can operate faster when frequently accessed data is preloaded.

### **Disadvantages**:

1. **Memory Overhead**: May cache unused or stale data, wasting resources.
2. **Long Startup Times**: Preloading can delay system initialization.

### **Use Cases**:

- Applications with predictable or frequent access patterns.
- Data that is frequently read but rarely updated.

### example: crickbuzz cricket score

```jsx
function preloadCache(keys) {
    keys.forEach(key => {
        const value = fetchFromSource(key); // Fetch from source
        cache.set(key, value); // Populate cache
    });
}

```

## Ways to Scale A cache(Same as Database)