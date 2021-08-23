(this page is a work in progress)

# Tests

Run the tests in the browser by loading `flow.html`.

Each class under `src/` should have a related test under `tests/`. For example, `src/easyscore.ts` is tested by `tests/easyscore_tests.ts`.


Suppose you just implemented a new VexFlow class called `Hello` in `src/hello.ts`.

- To create `tests/hello_tests.ts`, you can copy one of the existing test files (e.g., `tests/barline_tests.ts`.
- Modify `run.ts` to import your test module, and add a line to VexFlowTests.run() to invoke your `HelloTests.Start();`

## Other

If you are testing the private properties of a class, TypeScript and eslint will complain. You can temporarily silence these warnings by adding these lines to the top of your test file:

```
/* eslint-disable */
// @ts-nocheck
```