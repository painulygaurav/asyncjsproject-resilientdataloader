# Project: Resilient Data Loader (Promises and async/await)

## What to build

Write five small utilities in vanilla JS, using DummyJSON as the API, then wire them to a simple page.

| #   | Utility                    | What it does                                                           | Concept it solidifies                                            |
| --- | -------------------------- | ---------------------------------------------------------------------- | ---------------------------------------------------------------- |
| 1   | `wait(ms)`                 | Returns a promise that resolves after `ms`                             | Creating promises with `new Promise`                             |
| 2   | `fetchJson(url)`           | `fetch`, check `response.ok`, then `.json()`; throws on HTTP errors    | The `fetch` two-promise flow, and `fetch` not rejecting on a 404 |
| 3   | `withTimeout(promise, ms)` | Rejects if the promise takes longer than `ms`                          | `Promise.race`                                                   |
| 4   | `retry(fn, times, delay)`  | Calls `fn`; on failure waits and tries again, up to `times`            | `async/await`, `try/catch`, loops                                |
| 5   | `fetchMany(ids)`           | Loads many products in parallel and reports which succeeded and failed | `Promise.all` vs `Promise.allSettled`                            |

## The page

A single button, **Load products 1 to 10**, drives the whole page.

- Show a "Loading..." state while requests run.
- Then show the product list, with any failed IDs listed separately.
- Use `try/catch/finally`, with `finally` hiding the loader.

## Build order

Build and test each utility on its own before touching the page.

1. Write and test `wait` and `fetchJson` in the console.
2. Add `withTimeout` and test it with `wait(3000)` against a 1s limit.
3. Add `retry` and test it with a function that fails twice and then succeeds.
4. Add `fetchMany` using `allSettled` over IDs that include a bad one like `99999`, which returns a 404.
5. Wire everything to the page.

## Prove you understand it

Run these experiments, then explain each result to yourself.

- Load 10 products sequentially with `await` in a loop, then with `Promise.all`, and time both with `console.time`.
- Swap `allSettled` for `all` and watch one bad ID break everything.
- Try `items.forEach(async ...)` on purpose to see why it doesn't wait.
- Add a stray `console.log` after a `setTimeout`, a `.then()`, and an `await`, and predict the output order before running it.

## Stretch

Optional extras if you want more.

- Cancel an in-flight request with `AbortController`.
- Add a `Promise.any` "fastest mirror wins" call across two URLs.
