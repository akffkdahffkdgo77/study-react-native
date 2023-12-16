# TIL - React Native Bottom Sheet

<img width="400" alt="bottom sheet example" src="https://github.com/akffkdahffkdgo77/study-react-native/assets/52883505/fbb306b4-056d-464d-93e3-96f820d08483">

## 공식 사이트
- https://gorhom.github.io/react-native-bottom-sheet/ 
- https://gorhom.github.io/react-native-bottom-sheet/modal

### 설치

```

npm install @gorhom/bottom-sheet@^4
npm install react-native-reanimated react-native-gesture-handler

```

#### React Native Gesture Handler
- https://docs.swmansion.com/react-native-gesture-handler/docs/fundamentals/installation

```jsx
// App.tsx

<GestureHandlerRootView className="flex-1">
  <NavigationContainer>
    <StackNavigation />
  </NavigationContainer>
</GestureHandlerRootView>
```

#### React Native Reanimated
- https://docs.swmansion.com/react-native-reanimated/docs/fundamentals/getting-started/

**babel.config.js**

```

plugins: [
  'nativewind/babel',
  'react-native-reanimated/plugin',
]

```

### 실행하기 전

**Cache 삭제**

```

npm start --reset-cache

```

**IOS**

```

npx pod-install ios

```

## Code Example

```jsx
const bottomSheetModalRef = useRef<BottomSheetModal>(null);  // ref
const snapPoints = useMemo(() => ['50%'], []); // variables

// callbacks
const handlePresentModalPress = useCallback(() => {
  bottomSheetModalRef.current?.present();
}, []);

const handleSheetChanges = useCallback((index: number) => {
  console.log('handleSheetChanges', index);
}, []);

// backdrop
const renderBackdrop = useCallback(
  (props: any) => (
    <BottomSheetBackdrop
      {...props}
      pressBehavior="close"
      appearsOnIndex={0}
      disappearsOnIndex={-1}
      onPress={onClose}
    />
  ),
  [onClose],
);

return (
    <BottomSheetModal
        handleComponent={null} // 제거하면 pull up/down 못함
        ref={bottomSheetModalRef}
        index={0}
        snapPoints={snapPoints}
        onChange={handleSheetChanges}
        backdropComponent={renderBackdrop}
        style={styles.bottomSheetModal}
    >
    // children
   </BottomSheetModal>
);
```

## 비고

### Provider 추가
- 이렇게 최상단에 Provider를 넣어야 Header 위로 Overlay가 생김 ([링크](https://github.com/gorhom/react-native-bottom-sheet/issues/502#issuecomment-912971763))

```jsx
// App.tsx
<GestureHandlerRootView className="flex-1">
  <BottomSheetModalProvider>
    <NavigationContainer>
      <StackNavigation />
    </NavigationContainer>
  </BottomSheetModalProvider>
</GestureHandlerRootView>
```

## References
- https://ddioniii.tistory.com/50
- https://gorhom.github.io/react-native-bottom-sheet/modal/usage
