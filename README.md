# Study React Native

2023-12-04 ~ 2023-12-31
차기 RN 프로젝트에서 사용할 라이브러리 정리

## Version
react-native v0.72.7   
node v18   
npm 사용

## TIL

<details>
  <summary>
    <h3>NativeWind</h3>
  </summary>

  _RN에서 TailwindCSS 사용하기 위해서 사용_
  
  #### 공식 사이트
  [NativeWind](https://www.nativewind.dev/quick-starts/react-native-cli)
  
  #### 라이브러리 설치
  nativewind version 2 사용
  
  ```
  npm install nativewind
  npm install --save-dev tailwindcss
  npx tailwindcss init
  ```
  
  **!! 만약 에러가 난다면**
  npm run start를 했을 때 에러가 발생한다면...
  
  ```
  npm install tailwindcss@3.3.2 --save-dev
  ```
  
  #### tailwind.config.js
  content 수정
  
  ```
  content: ["./App.{js,jsx,ts,tsx}", "./src/**/*.{js,jsx,ts,tsx}"],
  ```
  
  #### babel.config.js
  plugin 수정
  
  ```
  plugins: ["nativewind/babel"]
  ```
  
  #### index.css 파일 추가
  src/styles에 index.css 파일 생성
  
  ```
  @tailwind base;
  @tailwind components;
  @tailwind utilities;
  ```
  
  #### postcss.config.js
  npm install --save-dev postcss autoprefixer
  postcss.config.js 파일 생성
  
  ```
  module.exports = {
    plugins: [require("tailwindcss"), [require("nativewind/postcss")]],
  };
  
  ```
  
  #### Tailwind CLI
  
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
  
  import "./nativewind-output"
  ```
  
  ```
  // package.json
  
  {
    "watch:css" : "npx tailwindcss -i src/styles/index.css --postcss postcss.config.js",
    "start" : "npm run watch:css & react-native start"
  }
  ```
</details>

<details>
  <summary>
    <h3>React Native Modal</h3>
  </summary>
  
  _기본 제공되는 Modal보다 더 많은 기능 제공_

  #### 공식 사이트
  
  [React Native Modal](https://github.com/react-native-modal/react-native-modal#usage)

  #### 설치
  
  ```
  npm install react-native-modal
  ```

  #### 기타
  -  ```backdropTransitionOutTiming={0}``` 으로 설정하면 모달이 깜빡거리면서 노출/미노출되는 현상 해결 가능   
  -  Full width / height으로 설정하고 싶으면 ```margin : 0```   
  -  ```onBackdropPress``` 로 backdrop(overlay) 클릭 시 모달이 닫히도록 설정 가능   
  -  ```justify-end```로 style 주면 모달이 하단에서 노출되도록 할 수 있음   
  
</details>
