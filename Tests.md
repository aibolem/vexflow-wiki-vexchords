(this page is a work in progress)

# Tests

Run the tests in the browser by loading `flow.html`.

Each class under `src/` should have a related test under `tests/`. For example, `src/easyscore.ts` is tested by `tests/easyscore_tests.ts`.


Suppose you just implemented a new VexFlow class called `Hello` in `src/hello.ts`.

- To create `tests/hello_tests.ts`, you can copy one of the existing test files (e.g., `tests/barline_tests.ts`.
- Modify `run.ts` to import your test module, and add a line to VexFlowTests.run() to invoke your `HelloTests.Start();`

## Other

If you are testing the internals of a class (e.g., private properties), TypeScript and eslint may complain.

You can disable warnings one line at a time with:
```
// eslint-disable-next-line
// @ts-ignore
obj.privateField = '123';
```

In extreme circumstances, you can silence TypeScript and eslint warnings for an entire test file by adding these lines to the top of the file:

```
/* eslint-disable */
// @ts-nocheck

obj.privateField = '123';
obj = unrelatedObjectWithDifferentType;

```

