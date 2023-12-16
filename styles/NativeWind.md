# TIL - NativeWind

_**RN**에서 **TailwindCSS** 사용하기 위해서 사용_

#### 비고
- Arbitrary Values보다 config 파일에 custom style을 추가해야 console에 warning 발생 x
- 외부 라이브러리는 className을 props로 받지 않고 StyleSheet를 사용해야하는 경우도 있음
- RN Component마다 지원하는 style 종류가 다름
  - ```leading-[15px]``` 이렇게 작성하면 warning 발생
  - **Image** 컴포넌트 사용시 **className**에 ```border border-black```을 추가하면 오류 발생

---

## 공식 사이트
[NativeWind](https://www.nativewind.dev/quick-starts/react-native-cli)

### 라이브러리 설치
nativewind version 2 사용

```
npm install nativewind
npm install --save-dev tailwindcss
npx tailwindcss init
```

#### !! 만약 에러가 난다면

npm run start를 했을 때 에러가 발생한다면...

```

npm install tailwindcss@3.3.2 --save-dev

```

### TypeScript
최상단에 declarations.d.ts 파일 생서

```

/// <reference types="nativewind/types" />

```

### tailwind.config.js
content 수정

```

content: ["./App.{js,jsx,ts,tsx}", "./src/**/*.{js,jsx,ts,tsx}"],

```

### babel.config.js
plugin 수정

```

plugins: ["nativewind/babel"]

```

### index.css 파일 추가
src/styles에 index.css 파일 생성

```

@tailwind base;
@tailwind components;
@tailwind utilities;

```

### postcss.config.js
npm install --save-dev postcss autoprefixer
postcss.config.js 파일 생성

```

module.exports = {
  plugins: [require("tailwindcss"), [require("nativewind/postcss")]],
};

```

### Tailwind CLI

```
// tailwind.config.js 수정

const nativewind = require("nativewind/tailwind/native")

module.exports = {
  content: ["./App.{js,jsx,ts,tsx}", "./src/**/*.{js,jsx,ts,tsx}"],
  plugins: [nativewind()], // 이 부분 추가
};
```

```
// postcss.config.js

// 이 부분 추가
module.exports = {
  plugins: {
    "nativewind/postcss": {
      output: "nativewind-output.js",
    },
  },
};
```

```
// index.js

import "./nativewind-output";

```

```
// package.json

{
  "watch:css" : "npx tailwindcss -i src/styles/index.css --postcss postcss.config.js",
  "start" : "npm run watch:css & react-native start"
}
```
