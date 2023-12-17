# TIL - React Native Permissions

IOS, Android Permissions

## 공식 사이트
- https://github.com/zoontek/react-native-permissions

### 설치

```

npm install react-native-permissions

```

## 비고
- **IOS**는 Podfile을 수정한 다음 ```npx pod-install ios``` 실행 ([참고](https://github.com/zoontek/react-native-permissions?tab=readme-ov-file#ios))
  + Info.plist에서 사용할 permission을 등록해줘야 함
- **Android**는 AndroidManifest.xml 파일에 permission 추가해줘야 함 ([참고](https://github.com/zoontek/react-native-permissions?tab=readme-ov-file#android))
