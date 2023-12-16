# TIL - React Native Linear Gradient 

이미지에 Linear Gradient 적용하기 위해서 사용

## 공식 사이트
- https://github.com/react-native-linear-gradient/react-native-linear-gradient

### 설치

```

npm install react-native-linear-gradient
npx pod-install ios

```

## Code Example
이미지에 하얀색 Linear Gradient 적용하기

```jsx
import { ImageBackground, View, StyleSheet } from 'react-native';
import LinearGradient from 'react-native-linear-gradient';

const LinearGradientExample = () => {
    return (
        <View className="flex-1 justify-center px-1">
            <ImageBackground
              borderTopLeftRadius={8}
              borderTopRightRadius={8}
              className="w-full h-full"
              source={{ uri: 'https://picsum.photos/id/237/200/300' }} // placeholder photo from Lorem Picsum
            >
              <LinearGradient
                start={{ x: 0, y: 0.5 }} // 0에서 시작하면 full height
                end={{ x: 0, y: 1 }}
                colors={['#FFFFFF00', '#FFFFFF']}
                style={styles.linearGradient}
              />
            </ImageBackground>
        </View>
    );
}

export default LinearGradientExample;

const styles = StyleSheet.create({
  linearGradient: {
    zIndex: 10,
    flex: 1,
    paddingLeft: 15,
    paddingRight: 15,
    borderRadius: 5,
  },
});

```
