# TIL - React Native Netinfo

디바이스 네트워크 연결 관리하기

## Version
React v18.2.0

React Native v0.72.7

React Native Netinfo v11.2.0

## 공식 사이트
- https://github.com/react-native-netinfo/react-native-netinfo

### 설치

```

npm install @react-native-community/netinfo
npx pod-install ios

```

### 사용 방법

hook으로 만들어서 사용하기

```jsx
// hooks/useNetwork.ts

import { useEffect } from 'react';
import NetInfo from '@react-native-community/netinfo';
import { Alert } from 'react-native';

const useNetwork = () => {
  useEffect(() => {
    const unsubscribe = NetInfo.addEventListener(({ isConnected }) => {
      if (!isConnected) {
        Alert.alert(
          '네트워크 연결이 끊겼습니다. 디바이스 연결 상태를 확인해주세요.',
        );
      } else {
        console.log('네트워크 연결 완료');
      }
    });

    return () => unsubscribe();
  }, []);
};

export default useNetwork;
```

```jsx
// App.tsx

useNetwork();

```

## References
- https://adjh54.tistory.com/210
