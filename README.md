# Study React Native

2023-12-04 ~   
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
