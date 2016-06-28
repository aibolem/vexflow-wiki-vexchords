# Steps

1. Run code through [`Lebab`](https://github.com/mohebifar/lebab) with `lebab <filepath> -o <filepath>`
  - [`Lebab`](https://github.com/mohebifar/lebab) is an ES5 to ES6 converter.
  - You can install it with `npm`. 
  - It seems to work quite well, but be sure to review the result because some transforms are unsafe.

2. Run `eslint --fix` <file>
  - This will fix some pretty trivial things, but definitely saves time.

3. Manual edits
  - Despite the automated bits, many errors will remain.

# Config

Here's the current `.eslintrc`, acquaint yourself with the [eslint rules](http://eslint.org/docs/rules/) and feel free to make suggestions. Note that we're extending the [`eslint-config-airbnb-base`](https://www.npmjs.com/package/eslint-config-airbnb-base)

```json
{
  "extends": "airbnb-base",
  "root": true,
  "rules": {
    "max-len": [2, 100],
    "camelcase": [0],
    "no-case-declarations": [2],
    "no-confusing-arrow": [0],
    "new-cap": [0],
    "no-else-return": [0],
    "no-multi-spaces": [0],
    "no-param-reassign": [0],
    "no-shadow": [0],
    "no-use-before-define": [0],
    "prefer-template": [0],
    "space-before-function-paren": [2, "never"],
    "strict": [2, "global"]
  }
}
```