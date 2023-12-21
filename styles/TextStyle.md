# TIL - Text Style

## Custom Font 적용하기
- `src/assets/fonts`에 폰트 파일 추가하기
- **react-native.config.js** 파일 추가하기

  ```js
  module.exports = {
    project: {
      ios: {},
      android: {},
    },
    assets: ['./src/assets/fonts'],
  };
  ```
  
- `npx react-native-assets` 해서 링크하기 ([참고1](https://stackoverflow.com/questions/72863402/npx-react-native-link-command-not-working-in-latest-version-of-react-native-how), [참고2](https://www.npmjs.com/package/react-native-asset))

### Android Font Family Issue
- Android와 IOS에서 Custom Font 적용하는 방법이 다름 ([참고](https://mniyunsu.github.io/react-native-fontfamily/))

  ```ts
  export const font500 = StyleSheet.create({
    ...Platform.select({
      ios: {
        fontFamily: 'Pretendard',
        fontWeight: '500',
      },
      android: {
        fontFamily: 'Pretendard-Medium',
      },
    }),
  });
  ```

## 기타 Style

### Line Height
- tailwindcss의 `leading-normal`은 사용할 수 없음
- **font-size**와 **line-height**를 함께 적용
