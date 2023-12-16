# TIL - React Native SVG

## 공식 사이트

- https://github.com/software-mansion/react-native-svg/blob/main/USAGE.md#usage

### 설치

```

npm install react-native-svg
npx pod-install ios

```

#### React Native SVG Transformer

- https://github.com/kristerkari/react-native-svg-transformer

```

npm install --save-dev react-native-svg-transformer

```

**metro.config.js**

- https://github.com/kristerkari/react-native-svg-transformer?tab=readme-ov-file#for-react-native-v0721-or-newer

```js
const { getDefaultConfig, mergeConfig } = require('@react-native/metro-config');

// https://github.com/kristerkari/react-native-svg-transformer#for-react-native-v0721-or-newer
const defaultConfig = getDefaultConfig(__dirname);
const { assetExts, sourceExts } = defaultConfig.resolver;

/**
 * Metro configuration
 * https://facebook.github.io/metro/docs/configuration
 *
 * @type {import('metro-config').MetroConfig}
 */
const config = {
  // https://github.com/kristerkari/react-native-svg-transformer#for-react-native-v0721-or-newer
  transformer: {
    babelTransformerPath: require.resolve('react-native-svg-transformer'),
  },
  resolver: {
    assetExts: assetExts.filter((ext) => ext !== 'svg'),
    sourceExts: [...sourceExts, 'svg'],
  },
};

module.exports = mergeConfig(defaultConfig, config);
```

**declarations.d.ts**

- https://github.com/kristerkari/react-native-svg-transformer?tab=readme-ov-file#using-typescript

```ts
declare module '*.svg' {
  import React from 'react';
  import { SvgProps } from 'react-native-svg';
  const content: React.FC<SvgProps>;
  export default content;
}
````

## SVG 사용 방법
- svg 파일에서 path의 fill을 **currentColor**로 변경하기

```ts
// assets/icons/index.ts

import HomeIcon from './ic_home.svg';

export const Icons = {
  Home: HomeIcon,
};

```

```jsx

<Icons.Home width={20} height={20} className="text-gray-500" />

```

## 비고
- 모든 설정을 한 다음 npm start 하기
