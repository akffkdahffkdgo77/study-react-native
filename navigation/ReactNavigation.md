# TIL - React Navigation
- [x] Stack Navigation
- [x] Bottom Tab Navigation
- [x] Nested Routing

## 공식 사이트
- https://reactnavigation.org/docs/getting-started

### 설치

```

npm install @react-navigation/native
npm install react-native-screens react-native-safe-area-context
npx pod-install ios

```

#### Stack Navigation 설치
- https://reactnavigation.org/docs/stack-navigator#installation

```

npm install @react-navigation/stack
npm install react-native-gesture-handler
npx pod-install ios

```

**index.js**

```js
import 'react-native-gesture-handler';
```

#### Bottom Navigation 설치
- https://reactnavigation.org/docs/bottom-tab-navigator#installation

```

npm install @react-navigation/bottom-tabs
npx pod-install ios

```

## Code Example

### Root Stack Navigator

```tsx
import { Image, Platform } from 'react-native';

import { createStackNavigator } from '@react-navigation/stack';
import { useSafeAreaInsets } from 'react-native-safe-area-context';

import Icons from '@assets/icons'; // icon 폴더
import { Screen } from '@config/screen'; // screen명 config

export type RootStackParamList = {
  [Screen.LANDING]: undefined;
  [Screen.MAIN]: undefined;
  [Screen.HOME]: undefined;
};

const Stack = createStackNavigator<RootStackParamList>();

const RootStackNavigation = () => {
    const insets = useSafeAreaInsets();

    return (        
        <Stack.Navigator
              initialRouteName={Screen.LANDING}
              screenOptions={{
                headerBackTitleVisible: false, // back 버튼에서 타이틀 텍스트 없애기
                headerTitleStyle: {
                  color: '#000000',
                  fontWeight: 'bold',
                  fontSize: 20,
                },
                headerStyle: {
                  height: 56 + insets.top,
                  backgroundColor: '#ffffff',
                  shadowColor: 'transparent',
                  borderBottomWidth: 0.6,
                  borderBottomColor: '#eeeeee',
                },
                headerTitleContainerStyle: {
                  marginHorizontal: 0, // margin 초기화
                },
                headerLeftContainerStyle: {
                  marginHorizontal: 0, // margin 초기화
                },
                headerRightContainerStyle: {
                  marginHorizontal: 0, // margin 초기화
                },
                headerTitleAlign: 'center',
                headerBackImage: () => (
                  <Image
                    source={Icons.ChevronLeft}
                    className={Platform.OS === 'android' ? 'ml-[3px]' : 'ml-4'} // android일 경우 marginVertical: 3, marginHorizontal: 11 하드코딩 되어있음
                  />
                ),
              }}
            >
              <Stack.Screen
                name={Screen.LANDING}
                component={LandingScreen}
                options={{ headerShown: false }}
              />
              <Stack.Screen
                name={Screen.MAIN}
                component={TabNavigation}
                options={{ headerShown: false }}
              />
        </Stack.Navigator>
    );
}

export default RootStackNavigation;
```

### Tab Navigator & Nested Routing

```tsx
import { createBottomTabNavigator } from '@react-navigation/bottom-tabs';
import { useSafeAreaInsets } from 'react-native-safe-area-context';

import { Icons } from '@assets/icons';
import { Screen } from '@config/screen';

export type TabNavParamList = {
  [Screen.HOME_TAB]: undefined;
};

const Tab = createBottomTabNavigator<TabNavParamList>();

const TabNavigation = () => {
    const insets = useSafeAreaInsets();

    return (
        <Tab.Navigator
            initialRouteName={Screen.HOME_TAB}
            screenOptions={{
              unmountOnBlur: true, // reset tab stack after moving to different tab
              headerTitleStyle: {
                color: '#000000',
              },
              headerStyle: {
                backgroundColor: '#fff',
                height: insets.top + 56,
              },
              headerTitleAlign: 'left',
            }}
          >
            <Tab.Screen
              name={Screen.HOME_TAB}
              component={HomeStackNavigation}
              options={{
                title: '홈',
                headerShown: false,
                tabBarIcon: (props) => <Icons.Home {...props} />,
                tabBarActiveTintColor: 'hotpink',
                tabBarInactiveTintColor: 'pink',
                tabBarLabel: '홈',
                tabBarLabelStyle: { color: 'black', fontSize: 13 },
                tabBarStyle: {
                  alignItems: 'flex-start',
                  justifyContent: 'flex-start',
                  height: 72 + insets.bottom,
                  paddingTop: 8,
                  paddingBottom: 8 + insets.bottom, // insets만큼 더해서 tab이 하단에 너무 붙어있지 않도록 설정
                },
              }}
            />
        </Tab.Navigator>
    );
}

export default TabNavigation;
```

```tsx
import { Image, Platform } from 'react-native';

import { createStackNavigator } from '@react-navigation/stack';
import { Images } from 'assets/images';
import { useSafeAreaInsets } from 'react-native-safe-area-context';

import { Icons } from '@assets/icons';
import { HomeHeaderButtons } from '@components/ActionBar';
import { Screen } from '@config/screen';

const Stack = createStackNavigator<RootStackParamList>();

const HomeStackNavigation = () => {
    return (
        <Stack.Navigator
          initialRouteName={Screen.HOME}
          screenOptions={{
            headerBackTitleVisible: false,
            headerStyle: {
              height: 56 + insets.top,
              backgroundColor: '#fff',
            },
            headerTitleContainerStyle: {
              marginHorizontal: 0, // margin 초기화
            },
            headerLeftContainerStyle: {
              marginHorizontal: 0, // margin 초기화
            },
            headerRightContainerStyle: {
              marginHorizontal: 0, // margin 초기화
            },
            headerTitleAlign: 'center',
            headerBackImage: () => (
              <Image
                source={Icons.ChevronLeft}
                className={Platform.OS === 'android' ? 'ml-[3px]' : 'ml-4'}
              />
            ),
          }}
        >
          <Stack.Screen
            name={Screen.HOME}
            component={HomeScreen}
            options={({ navigation, route }) => ({
              headerTitle: () => <Image source={Images.Logo} className="ml-3" />,
              headerShown: true,
              headerTitleAlign: 'left',
              headerRight: () => (
                <HomeHeaderButtons navigation={navigation} route={route} />
              ),
            })}
          />
        </Stack.Navigator>
    );
}

export default HomeStackNavigation;
```

## 비고

### TypeScript
- https://reactnavigation.org/docs/typescript
 
### Safe Area
- https://reactnavigation.org/docs/handling-safe-area/
- useSafeAreaInsets을 사용해서 tab의 디자인이 일정하게 적용될 수 있도록

<div>
  <img width="400" alt="iPhone 15" src="https://github.com/akffkdahffkdgo77/study-react-native/assets/52883505/17984751-5c46-4219-b4fa-285f5bd07f0e">
  <img width="400" alt="android 33" src="https://github.com/akffkdahffkdgo77/study-react-native/assets/52883505/56844dde-04ef-4136-90a4-d689bdebd8be">
  <img width="400" alt="iPhone SE" src="https://github.com/akffkdahffkdgo77/study-react-native/assets/52883505/4579c2c3-ea08-4d8f-aa92-a119c4a9ffeb">
</div>

### Tab Stack Navigation 초기화 하는 방법
- https://github.com/react-navigation/react-navigation/issues/8768#issuecomment-723150055

### Header에서 shadow만 없애기
- https://github.com/react-navigation/react-navigation/issues/865#issuecomment-324498672

### 기타
- ```headerShadowVisible: false``` 이렇게 설정하면 shadow + border 모두 미노출
