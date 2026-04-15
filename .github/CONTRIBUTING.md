# Contributing to react-native-modal-fix

Thanks for contributing.

`react-native-modal-fix` is a maintained fork of [`react-native-modal`](https://github.com/react-native-modal/react-native-modal). This repo focuses on safe bug fixes, compatibility updates, and release hygiene while keeping the API stable.

## Before you start

1. Search existing [issues](https://github.com/rjrajujha/react-native-modal-fix/issues) and [pull requests](https://github.com/rjrajujha/react-native-modal-fix/pulls).
2. For behavior that appears to come from React Native core `<Modal />`, include that detail in your report.
3. Prefer focused PRs with one logical change.

## Local development

1. Install dependencies in the root project:

```bash
npm install
```

2. Start TypeScript watch mode (optional while editing):

```bash
npm run dev
```

3. Validate changes before opening a PR:

```bash
npm run test
npm run build
```

## Working with the example app

```bash
cd example
npm install
npm run start
```

Then open `example/android` in Android Studio or `example/ios` in Xcode.

## Commit style

Conventional commit prefixes are used for release automation:

- `fix`: bug fix
- `feat`: feature
- `docs`: documentation only
- `refactor`: internal change without behavior change
- `perf`: performance improvement
- `test`: tests only
- `ci`: CI/CD changes
- `chore`: maintenance changes

## Pull request checklist

- [ ] Change is backward compatible, or migration notes are included.
- [ ] `npm run test` passes locally.
- [ ] `npm run build` passes locally.
- [ ] README/docs are updated when behavior or API changed.
- [ ] Any edge cases and tradeoffs are documented in the PR description.

## Release process

Releases are automated with Semantic Release from `main`.

## License

By contributing, you agree that your contributions will be licensed under the MIT license.
