# TIL - React Native Slider

Two Thumbs Range Slider 만들기

<img width="400" alt="range slider example" src="https://github.com/akffkdahffkdgo77/study-react-native/assets/52883505/597ab909-3d26-4628-b4f1-65a511b66da9">

## 공식 사이트
- https://github.com/miblanchard/react-native-slider#install


### 설치

```

npm install @miblanchard/react-native-slider

```

## Code Example

[참고](https://snack.expo.dev/@miblanchard/@miblanchard-react-native-slider)

Thumb 이미지를 변경하고 position을 다시 지정해줘야 함

```jsx
import { useState, Children, cloneElement } from 'react';
import { Image, View, StyleSheet } from 'react-native';

import { Slider } from '@miblanchard/react-native-slider';

import Images from '@assets/images'; // image assets 폴더

const SliderContainer = (props: { children: React.ReactElement }) => {
  const renderChildren = () => {
    return Children.map(props.children, (child: React.ReactElement) => {
      if (!!child && child.type === Slider) {
        return cloneElement(child);
      }
      return child;
    });
  };

  return (
    <View>
        {renderChildren()}
    </View>
  );
};

const TwoThumbsRangeSliderExample = () => {
    const [range, setRange] = useState([0, 10]);

    return (
        <SliderContainer>
          <Slider
            containerStyle={sliderStyle.container}
            trackClickable={true}
            renderThumbComponent={() => (
              <Image
                width={20}
                height={20}
                source={Images.SliderThumb}
                className="absolute -top-[18px] -left-4"
              />
            )}
            animateTransitions
            value={range}
            onSlidingComplete={setRange}
            maximumTrackTintColor="#FFFFFF"
            maximumValue={10}
            minimumTrackTintColor="#000000"
            minimumValue={0}
            step={1}
          />
        </SliderContainer>
    );
}

export default TwoThumbsRangeSliderExample;

const sliderStyle = StyleSheet.create({
  container: {
    marginHorizontal: 10,
  },
});

```
