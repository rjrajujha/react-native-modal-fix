# react-native-modal-fix

[![npm version](https://img.shields.io/npm/v/react-native-modal-fix.svg)](https://www.npmjs.com/package/react-native-modal-fix)
[![license](https://img.shields.io/npm/l/react-native-modal-fix.svg)](./LICENSE)

A maintained fork of [`react-native-modal`](https://github.com/react-native-modal/react-native-modal) for teams that need a stable, drop-in modal API with targeted fixes.

If you are happy with the upstream package, use it. If you are blocked by fork-specific fixes or maintenance needs, use `react-native-modal-fix`.

## What this package is

`react-native-modal-fix` extends React Native's built-in [`<Modal />`](https://reactnative.dev/docs/modal) with:

- enter/exit animations
- swipe to dismiss
- backdrop customization
- lifecycle callbacks
- keyboard avoidance and orientation support

## What issue this fork solves

This fork keeps the original API but addresses practical maintenance gaps for production apps, including:

- compatibility updates around dimension change subscriptions across React Native versions
- swipe/scroll edge-case handling improvements
- stable backdrop behavior and animation flow
- modernized release and package metadata hygiene

## Why use this fork

Use this package when you need:

- a mostly drop-in replacement for `react-native-modal`
- conservative, targeted fixes without a full rewrite
- predictable npm package metadata and release setup

## Installation

```bash
npm install react-native-modal-fix
```

or

```bash
yarn add react-native-modal-fix
```

## Quick usage

```tsx
import React, {useState} from 'react';
import {Button, Text, View} from 'react-native';
import Modal from 'react-native-modal-fix';

export default function Example() {
  const [visible, setVisible] = useState(false);

  return (
    <View style={{flex: 1, justifyContent: 'center'}}>
      <Button title="Show modal" onPress={() => setVisible(true)} />

      <Modal
        isVisible={visible}
        onBackdropPress={() => setVisible(false)}
        onBackButtonPress={() => setVisible(false)}>
        <View style={{backgroundColor: 'white', padding: 16, borderRadius: 8}}>
          <Text>Hello from react-native-modal-fix</Text>
          <Button title="Close" onPress={() => setVisible(false)} />
        </View>
      </Modal>
    </View>
  );
}
```

## API reference

`react-native-modal-fix` accepts all React Native `<Modal />` props plus the props below.

| Prop                             | Type                                                | Default                     | Description                                              |
| -------------------------------- | --------------------------------------------------- | --------------------------- | -------------------------------------------------------- |
| `isVisible`                      | `boolean`                                           | `false`                     | Controls visibility.                                     |
| `children`                       | `ReactNode`                                         | required                    | Modal content.                                           |
| `animationIn`                    | `string \| object`                                  | `'slideInUp'`               | Enter animation.                                         |
| `animationInTiming`              | `number`                                            | `300`                       | Enter animation duration (ms).                           |
| `animationOut`                   | `string \| object`                                  | `'slideOutDown'`            | Exit animation.                                          |
| `animationOutTiming`             | `number`                                            | `300`                       | Exit animation duration (ms).                            |
| `avoidKeyboard`                  | `boolean`                                           | `false`                     | Moves content up when keyboard opens.                    |
| `coverScreen`                    | `boolean`                                           | `true`                      | Renders through React Native `<Modal />`.                |
| `hasBackdrop`                    | `boolean`                                           | `true`                      | Shows backdrop.                                          |
| `backdropColor`                  | `string`                                            | `'black'`                   | Backdrop color.                                          |
| `backdropOpacity`                | `number`                                            | `0.7`                       | Backdrop opacity.                                        |
| `backdropTransitionInTiming`     | `number`                                            | `300`                       | Backdrop enter duration (ms).                            |
| `backdropTransitionOutTiming`    | `number`                                            | `300`                       | Backdrop exit duration (ms).                             |
| `customBackdrop`                 | `ReactNode`                                         | `null`                      | Custom backdrop component.                               |
| `onBackdropPress`                | `() => void`                                        | noop                        | Called when backdrop is pressed (default backdrop only). |
| `onBackButtonPress`              | `() => void`                                        | noop                        | Called on Android back press (`onRequestClose`).         |
| `onModalWillShow`                | `() => void`                                        | noop                        | Called before show animation.                            |
| `onModalShow`                    | `() => void`                                        | noop                        | Called after show animation.                             |
| `onModalWillHide`                | `() => void`                                        | noop                        | Called before hide animation.                            |
| `onModalHide`                    | `() => void`                                        | noop                        | Called after hide animation.                             |
| `swipeDirection`                 | `'up' \| 'down' \| 'left' \| 'right' \| Array<...>` | `undefined`                 | Enables swipe-to-dismiss directions.                     |
| `swipeThreshold`                 | `number`                                            | `100`                       | Distance threshold for swipe complete.                   |
| `onSwipeStart`                   | `(gestureState) => void`                            | noop                        | Swipe started callback.                                  |
| `onSwipeMove`                    | `(percentageShown, gestureState) => void`           | noop                        | Swipe move callback.                                     |
| `onSwipeComplete`                | `({ swipingDirection }, gestureState) => void`      | noop                        | Swipe completed callback.                                |
| `onSwipeCancel`                  | `(gestureState) => void`                            | noop                        | Swipe canceled callback.                                 |
| `panResponderThreshold`          | `number`                                            | `4`                         | Movement threshold before PanResponder engages.          |
| `scrollTo`                       | `({x?, y?, animated?}) => void`                     | `null`                      | Integrates swipe with scrollable content.                |
| `scrollOffset`                   | `number`                                            | `0`                         | Current scroll offset.                                   |
| `scrollOffsetMax`                | `number`                                            | `0`                         | Max scroll offset for overscroll handling.               |
| `scrollHorizontal`               | `boolean`                                           | `false`                     | Set `true` for horizontal scroll views.                  |
| `propagateSwipe`                 | `boolean \| (event, gestureState) => boolean`       | `false`                     | Lets child scroll views receive gestures.                |
| `useNativeDriver`                | `boolean`                                           | `false`                     | Uses native driver for content animation.                |
| `useNativeDriverForBackdrop`     | `boolean`                                           | `undefined`                 | Uses native driver for backdrop animation.               |
| `hideModalContentWhileAnimating` | `boolean`                                           | `false`                     | Hides content during native-driver animation.            |
| `deviceHeight`                   | `number`                                            | `null`                      | Overrides device height when needed.                     |
| `deviceWidth`                    | `number`                                            | `null`                      | Overrides device width when needed.                      |
| `supportedOrientations`          | `Orientation[]`                                     | `['portrait', 'landscape']` | Forwarded to RN `<Modal />`.                             |
| `style`                          | `StyleProp<ViewStyle>`                              | `undefined`                 | Modal content container style.                           |

### Deprecated prop

- `onSwipe` is still supported for compatibility but deprecated. Use `onSwipeComplete`.

## Compatibility and migration

### React Native support

- peer dependency: `react-native >= 0.65.0`
- peer dependency: `react >= 16.8.0`

### Migrating from `react-native-modal`

Most code is a direct import-path swap:

```diff
-import Modal from 'react-native-modal';
+import Modal from 'react-native-modal-fix';
```

No API redesign is required for typical usage.

## Known behavior notes

- This library still depends on React Native core `<Modal />`, so some platform quirks are upstream RN limitations.
- On some setups, `useNativeDriver={true}` with swipe gestures can feel imperfect; test gesture-heavy flows on target devices.

## Local development

```bash
npm install
npm run test
npm run build
```

Example app:

```bash
cd example
npm install
npm run start
```

## Publish checklist

Before publishing:

1. Run `npm run test` and `npm run build`.
2. Run `npm run pack:dry` and verify tarball contents.
3. Confirm `README`, `CHANGELOG.md`, and package metadata are current.
4. Publish from a clean `main` branch.

## Credit to original project

This package is a respectful fork of [`react-native-modal`](https://github.com/react-native-modal/react-native-modal), originally created and maintained by its contributors.

- Original repository: https://github.com/react-native-modal/react-native-modal
- Original npm package: https://www.npmjs.com/package/react-native-modal

If this fork does not solve your need, please also evaluate upstream.

## License

MIT - see [LICENSE](./LICENSE).
