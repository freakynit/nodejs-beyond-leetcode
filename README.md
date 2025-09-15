# Real-World Node.js Interview Questions

A collection of **interview questions** (and self-practise questions) designed to test **practical, real-world engineering skills** in Node.js and JavaScript.

These aren’t algorithm drills or textbook trivia - they’re based on challenges that actually show up when building and scaling systems.

---

## Examples

- Ensure only one request at a time is processed per email address in an Express app.  
- What happens if a producer writes to a stream faster than the consumer can read?  
- How can the event loop appear "frozen" without an infinite loop?  
- Implement a safe substitution mechanism for dynamic template strings.  
- Enforce concurrency limits when running 1000 async tasks.  

---

## Why this repo?

Most interview prep focuses on either:
- Basic trivia ("what does `this` mean here?"), or  
- Algorithm puzzles you’ll never implement again in your career.  

This repo is different: it focuses on **scenarios that represent real-world problems, free from tutorial-level knowledge**.

---

## Contributing

If you’ve hit a tricky Node.js bug or design challenge in production, turn it into a question!  
PRs welcome for:
- New unique questions  
- Improved clarity/explanations  
- Code examples illustrating solutions  

---

## License
The content of this repository is released under an open-source license. See the [LICENSE](LICENSE) file for details.

---

## Questions

- [Per-Email Request Serialization in Express](#per-email-request-serialization-in-express)
- [Implementing a Mutex in Node.js with async/await](#implementing-a-mutex-in-nodejs-with-asyncawait)
- [Race Conditions in a Single-Threaded Node.js Environment](#race-conditions-in-a-single-threaded-nodejs-environment)
- [Backpressure in Node.js Streams](#backpressure-in-nodejs-streams)
- [Freezing the Event Loop Without Infinite Loops](#freezing-the-event-loop-without-infinite-loops)
- [Template String Substitution in Node.js](#template-string-substitution-in-nodejs)
- [Finally Block and Response Delay in Express](#finally-block-and-response-delay-in-express)
- [Async Timeout and Cancellation in Node.js](#async-timeout-and-cancellation-in-nodejs)
- [Implementing a Countdown Latch in JavaScript](#implementing-a-countdown-latch-in-javascript)
- [Running Async Tasks with Concurrency Limits](#running-async-tasks-with-concurrency-limits)
- [Behavior of Array.from with Async Functions](#behavior-of-arrayfrom-with-async-functions)
- [Custom Mutex Implementation in Node.js](#custom-mutex-implementation-in-nodejs)
- [Finding the Largest Array in a Nested JSON Object](#finding-the-largest-array-in-a-nested-json-object)
- [Finding Path to Target Value in a Nested JSON Object](#finding-path-to-target-value-in-a-nested-json-object)
- [One-Liner Function to Chunk an Array](#one-liner-function-to-chunk-an-array)
- [Filtering Array of Objects by Matching URLs](#filtering-array-of-objects-by-matching-urls)
- [Data Masking and Unmasking](#data-masking-and-unmasking)
- [Handling Uncaught Exceptions in Async Code](#handling-uncaught-exceptions-in-async-code)
- [Graceful Shutdown in Node.js with In-Flight Requests](#graceful-shutdown-in-nodejs-with-in-flight-requests)
- [Caching Strategies for Dynamic Routes](#caching-strategies-for-dynamic-routes)
- [Debounced Function with Cancellation and Edge Invocation](#debounced-function-with-cancellation-and-edge-invocation)
- [API Retry Utility](#api-retry-utility)
- [Database Connection Pool](#database-connection-pool)
- [Bucketize Time-Series Data by Multiple Interval Sizes](#bucketize-time-series-data-by-multiple-interval-sizes)
- [Lazy vs. Eager Evaluation in Async Iterators](#lazy-vs-eager-evaluation-in-async-iterators)
- [Task Queue with Delayed and Scheduled Jobs](#task-queue-with-delayed-and-scheduled-jobs)
- [A Simple Dependency Injection (DI) container](#a-simple-dependency-injection-di-container)

---

### Per-Email Request Serialization in Express

In a Node.js application using Express, imagine you have an endpoint that accepts POST requests with an `email` field in the request body.

How would you design the request handler so that **only one request at a time is processed for a given email address**, while still allowing requests for different emails to be processed concurrently?

What considerations would you keep in mind if the service is scaled across multiple Node.js instances?

---

## Implementing a Mutex in Node.js with async/await

In JavaScript (Node.js), multiple asynchronous tasks may try to access and modify the same shared resource concurrently. How would you implement a simple mutex (mutual exclusion lock) in Node.js using `async/await` so that only one task can enter a critical section at a time?

**Note:** 
- The JavaScript execution thread (event loop) is single-threaded, so two pieces of JS code can’t literally run at the same time on different threads.
- But Node.js is asynchronous. Multiple async operations (e.g. I/O, DB queries, timers, worker threads, cluster processes) can complete at unpredictable times, and their callbacks may interleave in ways that still require synchronization at the application level.

---

### Race Conditions in a Single-Threaded Node.js Environment

JavaScript in Node.js runs on a single thread, but asynchronous operations can still cause unexpected behavior. Can you explain how race conditions can occur in a single-threaded environment like Node.js, and demonstrate with a small code example?

---

### Backpressure in Node.js Streams

What happens if a producer writes data to a Node.js stream faster than the consumer can read it? How does Node handle this, and how would you implement backpressure control in practice?

---

### Freezing the Event Loop Without Infinite Loops

Can you write a small snippet of code in Node.js that makes the event loop appear 'frozen' even though no synchronous infinite loop is running?

---

### Template String Substitution in Node.js

Suppose you have template strings stored in a file. The template variables are written in the same style as JavaScript template literals, for example: `"Hello ${name}, welcome to ${place}"`. At runtime, you need to load such a string and replace the variables with actual values provided in an object or dictionary.

How would you implement this substitution mechanism? Can you discuss both a safe/simple approach and whether JavaScript offers any native support for evaluating these template variables dynamically?

---

### Finally Block and Response Delay in Express

In your Express.js API, you have a route handler with this structure:

```jsx
app.get('/api/data', async (req, res) => {
  try {
    const result = await processData();
    return res.json(result);
  } catch (error) {
    return res.status(500).json({ error: 'Failed' });
  } finally {
    await insertToDatabase1();
    await insertToDatabase2();
  }
});

```

Will the database operations in the `finally` block delay the response being sent to the client? Why or why not?

- *Follow up if answer is yes: How can you prevent that blocking.*
    
    

---

### Async Timeout and Cancellation in Node.js

Suppose you’re working in Node.js, and you need to enforce a timeout on any asynchronous method call - even if that method comes from a third-party library where you don’t have access to the source code. How would you design a solution so that the async operation either completes within the timeout or fails with an error? Can you also discuss approaches for when the underlying library does or does not support cancellation?

---

### Implementing a Countdown Latch in JavaScript

In multithreaded environments like Java, a **Countdown Latch** is a synchronization aid that allows one or more threads to wait until a set of operations complete.

How would you implement a **simple countdown latch** in JavaScript/Node.js (which is single-threaded but has async concurrency)? Show how your implementation could be used to wait for multiple async operations before proceeding.

---

### Running Async Tasks with Concurrency Limits

You have an array of 1000 async tasks (functions returning Promises). If you just call `Promise.all`, you might overwhelm the system. How would you implement a function to run these tasks with a maximum concurrency limit of, say, 5 at a time?

---

### Behavior of Array.from with Async Functions

You’re given the following Node.js code:

```jsx
const tasks = Array.from({ length: 1000 }, (_, i) => async () => {
  await new Promise(r => setTimeout(r, 100)); // simulate async work
  return i;
});
```

- After this line executes, what exactly is stored in `tasks`?
- Does the construction of the array wait for the `setTimeout` promises to resolve before completing?
- How would the behavior change if the code were instead written as:

```jsx
const tasks = Array.from({ length: 1000 }, async (_, i) => {
  await new Promise(r => setTimeout(r, 100));
  return i;
});
```

---

### Custom Mutex Implementation in Node.js

In Node.js, multiple asynchronous functions may try to access or modify shared resources at the same time. How would you design and implement a simple mutex (mutual exclusion lock) to ensure that only one function can execute a critical section at a time? Please provide a code example.

---

### Finding the Largest Array in a Nested JSON Object

You are given a JSON object of arbitrary shape. This object can contain nested objects and arrays at any depth.

Write a function in JavaScript/Node.js that:

1. Recursively traverses the JSON object.
2. Identifies the array with the **largest number of immediate children** (not counting nested arrays within those children).
3. Returns both the **array itself** and the **key under which it is stored**.

Your function should work for deeply nested JSON objects, not just top-level arrays.

---

### Finding Path to Target Value in a Nested JSON Object

You are given a JSON object of arbitrary shape and a **target value**.

Write a function in JavaScript/Node.js that:

1. Recursively searches the object.
2. Returns the **path of keys** that leads to the first occurrence of the target value.
3. If the value does not exist, return `null`.

> For example, given `{ a: { b: { c: 42 } } }` and target `42`, the function should return `["a", "b", "c"]`.
> 

---

### One-Liner Function to Chunk an Array

You are given an array of items and a batch size. Write a function in **JavaScript/Node.js** that splits the array into smaller arrays ("batches"), each of the given batch size.

1. The function must be written as a one-liner.
2. You can skip handling for nulls.

Example:

```jsx
chunkArray([1, 2, 3, 4, 5, 6, 7], 3);
// Expected output: [[1,2,3], [4,5,6], [7]]
```

---

### Filtering Array of Objects by Matching URLs

You are given two arrays of objects in Node.js:

1. The first array (`arr1`) contains objects with `title` and `url`.
2. The second array (`arr2`) contains objects with `title`, `url`, and `content`.

Write a function that filters `arr2` so that it only contains the objects whose `url` is also present in `arr1`.

Example Input:

```jsx
const arr1 = [
  { title: "First", url: "<https://a.com>" },
  { title: "Second", url: "<https://b.com>" }
];

const arr2 = [
  { title: "First", url: "<https://a.com>", content: "Content A" },
  { title: "Third", url: "<https://c.com>", content: "Content C" },
  { title: "Second", url: "<https://b.com>", content: "Content B" }
];
```

**Expected Output:**

```jsx
[
  { title: "First", url: "<https://a.com>", content: "Content A" },
  { title: "Second", url: "<https://b.com>", content: "Content B" }
]
```

---

### Data Masking and Unmasking

Write a function in Node.js that:
1. Takes a buffer of data and a 4-byte masking key.
2. Returns a masked version of the data using XOR. Maksing should happen byte-by-byte
3. Then, demonstrate unmasking the same.
4. Why XOR and what are the benefits of masking like this?

Follow-up question:
1. Suppose instead of masking byte-by-byte, you want to optimize the process by applying the mask in 32-bit chunks. How would you do that?
2. This implementation should properly handle trailing bytes if the data length is not a multiple of 4.

---

### Handling Uncaught Exceptions in Async Code

In a Node.js application, uncaught exceptions in synchronous code can crash the process, but async code behaves differently. Explain how Node.js handles unhandled promise rejections, and provide a code example showing how to implement a global handler that logs errors without crashing the server.

---

### Graceful Shutdown in Node.js with In-Flight Requests

When running a Node.js server (using Express maybe), how would you implement a graceful shutdown so that:

1. New requests stop being accepted once a shutdown signal (SIGTERM) is received.
2. Existing in-flight requests are allowed to finish.
3. Any open database or message queue connections are properly closed.

Provide a minimal code example to demonstrate the implementation for this.

---

### Caching Strategies for Dynamic Routes

In an Express app with dynamic routes (e.g., /user/:id), you want to cache responses to reduce database load, but only for frequently accessed IDs. How would you implement an in-memory cache, with TTL expiration, a few eviction policies and cache invalidation on updates.

---

### Debounced Function with Cancellation and Edge Invocation

Imagine you're implementing a `search-as-you-type` feature in Node.js (for example, querying a database or triggering webhooks). To avoid flooding the system with unnecessary requests, you decide to use `debouncing`.

**Part 1:**

1. What is `debouncing`?
2. Why is it useful, and in what scenarios would debouncing be an appropriate choice?


**Part 2:**

Implement a utility function `debounceWithCancellation<T>()` that wraps an asynchronous function. The requirements are:

- Input: an async function `(...args) => T`.
- Output: a wrapped function that: Can be called as `(...args) => Promise<T>` and provides a `.cancel()` method to discard any pending invocation/request.

**Part 3:**

Enhance your implementation to support the following options:

1. `Trailing invocation` - Ensure the last call is eventually executed after the debounce delay (default behavior in many debounce utilities).
2. `Leading invocation` - Optionally allow immediate execution on the first call, then suppress further calls until the delay has passed.
3. `Configurable delay` - Allow the debounce delay to be set via an options object.

Updated function signature:

```
debounceWithCancellation<T>(
  fn: (...args: any[]) => Promise<T>,
  options: { leading?: boolean; trailing?: boolean; delay: number }
): ((...args: any[]) => Promise<T>) & { cancel: () => void }
```

---

### API Retry Utility

Design a `retry()` helper for external API calls that may fail with:

- `Retryable`: `429 Too Many Requests`, transient `5xx`, or network errors
- `Non-retryable`: All other `4xx`

The function should:

1. Accept: `asyncFn`, `maxRetries`, `backoffStrategy` (`linear`, `exponential`), and optional `jitter` value.
2. Logic:
  - No retries on `4xx` (except `429`)
  - Retry all `5xx`
  - For `429`, respect `Retry-After` if present, otherwise use `backoffStrategy`
3. Add `jitter` if given.
4. Support cancellation via `AbortSignal`

---

### Database Connection Pool

Design a `ConnectionPool` utility for managing database connections.

1. Maintain a fixed `maxConnections`
2. Reuse idle connections when available
2. Queue requests if the pool is exhausted

Timeouts:

1. `Connection timeout` – fail if a new connection can't be established in time
2. `Acquire timeout` – fail if a connection can’t be checked out from the pool in time
3. `Idle timeout` – close connections left unused for too long

Also:

1. Support `release()` to return a connection back to the pool
2. Support `destroy()` to close all connections

---

### Bucketize Time-Series Data by Multiple Interval Sizes

You are given an array of objects. Each object has:

1. a `timestamp` in ISO-8601 string format, and
2. a `data` field (which can hold any value, even complex objects).

You are also given an array of interval sizes (in seconds).

Write a function that takes such an array of objects and the array of interval sizes, and for each interval size, groups the objects into consecutive time buckets of that size.

1. Each bucket represents a time range based on the interval size.
2. The bucket "key" can be represented as the starting timestamp of that bucket (in epoch seconds, or ISO-8601).
3. If multiple objects fall into the same bucket, all of them should be grouped together under that bucket.
4. The function should return an object (or map) where keys are interval sizes, and values are the bucketized results for that interval size.

Example Input and Output:

Input:

```javascript
const items = [
  { data: "A", timestamp: "2025-09-13T12:00:01Z" },
  { data: "B", timestamp: "2025-09-13T12:00:04Z" },
  { data: "C", timestamp: "2025-09-13T12:00:08Z" },
  { data: "D", timestamp: "2025-09-13T12:00:12Z" }
];

const intervals = [5, 10];
```

Output:

```javascript
{
  5: {
    "2025-09-13T12:00:00Z": [{data:"A"}, {data:"B"}],
    "2025-09-13T12:00:05Z": [{data:"C"}],
    "2025-09-13T12:00:10Z": [{data:"D"}]
  },
  10: {
    "2025-09-13T12:00:00Z": [{data:"A"}, {data:"B"}, {data:"C"}],
    "2025-09-13T12:00:10Z": [{data:"D"}]
  }
}
```

---

### Lazy vs. Eager Evaluation in Async Iterators

When working with async iterators, what is the difference between `lazy evaluation` and `eager evaluation`? Can you illustrate with an example where lazy evaluation is more efficient than eager evaluation?

---


### Task Queue with Delayed and Scheduled Jobs

Design and implement a small task-queue system that supports:

1. Enqueuing immediate jobs.
2. Enqueuing delayed jobs (run once after a delay).
3. Enqueuing scheduled/recurring jobs (cron-style).
4. Reliable processing with retries and exponential backoff.
5. Graceful worker shutdown.
6. At-least-once delivery semantics (job may run more than once on failure).
7. Simple job deduplication to prevent identical jobs from being queued repeatedly.

---

### A Simple Dependency Injection (DI) container

Design a simple Dependency Injection (DI) container that supports `singleton` and `transient` lifetimes.

Your container should implement at least these two methods:

```ts
class Container {
  register(name: string, factory: (c: Container) => any, options?: { singleton?: boolean }): void;
  resolve<T = any>(name: string): T;
}
```
