# TIL - React Native Image Picker

RN에서 사진 올리기

## 공식 사이트
- https://github.com/react-native-image-picker/react-native-image-picker

### 설치

```

npm install react-native-image-picker
npx pod-install ios

```

### Post Install

#### IOS 
- **Info.plist**에 직접 등록해야 함 ([참고](https://deku.posstree.com/ko/react-native/react-native-image-picker/))

```
<key>NSCameraUsageDescription</key>
<string>$(PRODUCT_NAME) would like to use your camera</string>
<key>NSPhotoLibraryUsageDescription</key>
<string>$(PRODUCT_NAME) would like access to your photo gallery</string>
```

#### Android
- **AndroidManifest.xml**에 카메라 권한 등 추가

```xml
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.READ_MEDIA_IMAGES"/>
```

## 비고
- IOS simualtor에는 카메라 없음
- react-native-permissions 사용해서 카메라 / 앨범 사용 권한 획득하기

## References
- [axios로 업로드하기](https://velog.io/@horang-e/react-native-image-picker-%EB%A1%9C-%EA%B0%80%EC%A0%B8%EC%98%A8-%ED%8C%8C%EC%9D%BC-%EC%84%9C%EB%B2%84%EC%97%90-axios%EB%A1%9C-%EC%97%85%EB%A1%9C%EB%93%9C-%ED%95%98%EA%B8%B0)
