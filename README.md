# memorisable-js
A simple way to implement memorisable in JavaScript through caching and hash table 

## JavaScript

```js
const memorisable = (callback) => {
  const caches = {};

  return (...args) => {
    const cacheKey = JSON.stringify(args);

    if (caches[cacheKey]) {
      return caches[cacheKey];
    }

    caches[cacheKey] = callback.apply(globalThis, args);
    return caches[cacheKey];
  };
};

const sum = memorisable((a, b) => a + b);
sum(1, 2); // call function
sum(1, 2); // return value from cache
```


## TypeScript
```ts
const memorisable = <T extends (...args: Parameters<T>) => ReturnType<T>>(
  callback: T,
) => {
  const caches: Record<string, ReturnType<T>> = {};

  return (...args: Parameters<T>) => {
    const cacheKey = JSON.stringify(args);

    if (caches[cacheKey]) {
      return caches[cacheKey];
    }

    caches[cacheKey] = callback.apply(globalThis, args);
    return caches[cacheKey];
  };
};

const sum = memorisable((a: number, b: number) => a + b);
sum(1, 2); // call function
sum(1, 2); // return value from cache
```
