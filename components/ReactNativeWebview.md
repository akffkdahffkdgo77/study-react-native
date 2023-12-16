# TIL - React Native Webview

## 공식 사이트
- https://github.com/react-native-webview/react-native-webview/blob/master/docs/Getting-Started.md

### 설치

```

npm install --save react-native-webview
npx pod-install ios

```

### 설치 - Android

```
android/gradle.properties

// 이미 이렇게 설정되어 있긴 함!
android.useAndroidX=true
android.enableJetifier=true

```

## Code Example

```jsx
import { Dimensions } from 'react-native';
import WebView from 'react-native-webview';

const deviceHeight = Dimensions.get('window').height;
const deviceWidth = Dimensions.get('window').width;

const WebviewTest = () => {
    return (
      <WebView
        scalesPageToFit
        style={{ height: deviceHeight, width: deviceWidth }}
        className="flex-1"
        source={{ uri }}
      />
    );
}

export default WebviewTest;
```
