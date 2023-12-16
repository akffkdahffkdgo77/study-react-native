# TIL - React Native Reanimated Carousel 

## 공식 사이트
- https://github.com/dohooo/react-native-reanimated-carousel
- https://react-native-reanimated-carousel.vercel.app/

### 설치

```

npm install react-native-reanimated-carousel

// 이미 설치가 되어있고 설정 끝났으면 X
npm install react-native-reanimated react-native-gesture-handler

```

## Code Example

```jsx
import { View, Text, TouchableHighlight } from 'react-native';

import Carousel, { ICarouselInstance } from 'react-native-reanimated-carousel';

const CarouselExample = () => {
    const carouselRef = useRef<ICarouselInstance>(null);

    return (
        <View className="flex-1">
            <TouchableHighlight
              onPress={() => carouselRef.current?.prev()}
            >
              <Text>Prev</Text>
            </TouchableHighlight>
            <Carousel
              ref={carouselRef}
              loop
              width={width}
              autoPlay={true}
              data={[...new Array(6).keys()]}
              autoPlayInterval={3000}
              scrollAnimationDuration={1000}
              onSnapToItem={(index) => console.log('current index:', index)}
              renderItem={() => (
                <View className="flex-1 justify-center px-1">
                    <Text>Hello</Text>                   
                </View>
              )}
            />
            <TouchableHighlight
              onPress={() => carouselRef.current?.next()}
            >
              <Text>Next</Text>
            </TouchableHighlight>
        </View>
    );
}

export default CarouselExample;
```
