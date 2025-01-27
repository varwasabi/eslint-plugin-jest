# Prefer mock resolved/rejected shorthands for promises (`prefer-mock-promise-shorthand`)

💼 This rule is enabled in the following
[configs](https://github.com/jest-community/eslint-plugin-jest/blob/main/README.md#shareable-configurations):
`all`.

🔧 This rule is automatically fixable using the `--fix`
[option](https://eslint.org/docs/latest/user-guide/command-line-interface#--fix)
on the command line.

<!-- end rule header -->

When working with mocks of functions that return promises, Jest provides some
API sugar functions to reduce the amount of boilerplate you have to write.

These methods should be preferred when possible.

## Rule details

The following patterns are warnings:

```js
jest.fn().mockImplementation(() => Promise.resolve(123));
jest
  .spyOn(fs.promises, 'readFile')
  .mockReturnValue(Promise.reject(new Error('oh noes!')));

myFunction
  .mockReturnValueOnce(Promise.resolve(42))
  .mockImplementationOnce(() => Promise.resolve(42))
  .mockReturnValue(Promise.reject(new Error('too many calls!')));
```

The following patterns are not warnings:

```js
jest.fn().mockResolvedValue(123);
jest.spyOn(fs.promises, 'readFile').mockRejectedValue(new Error('oh noes!'));

myFunction
  .mockResolvedValueOnce(42)
  .mockResolvedValueOnce(42)
  .mockRejectedValue(new Error('too many calls!'));
```
