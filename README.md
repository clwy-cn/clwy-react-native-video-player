# react-native-clwy-video-player

A customisable, updated, React Native video player for Android and IOS, based on [abbasfreestyle react-native-af-video-player](https://github.com/abbasfreestyle/react-native-af-video-player) and 
[rbcorrea/react-native-rb-video-player](https://github.com/rbcorrea/react-native-rb-video-player).

This is a result of not merged pull requests and some modifications planned to be used with React Native 0.6+ version.

![Demo](./demo.gif)

## What did I do?
- Android 

It works good on Android. I resolved all warning and FullScreenControl disappear errors.

- iOS

In iOS，I recommend you to use [react-native-video](https://github.com/react-native-community/react-native-video) instead.

## Features

* Fullscreen support for Android and iOS!
* Works with react-navigation
* Optional action button for custom use
* Add your own logo and/or placeholder
* Customise theme

## Install

```shell
yarn add react-native-clwy-video-player react-native-orientation @sayem314/react-native-keep-awake
npx pod-install
```

## Props

Prop                  | Type     | Required | Default                   | Description
--------------------- | -------- | -------- | ------------------------- | -----------
url                   | string, number | Yes |                          | A URL string (or number for local) is required.
autoPlay              | bool     | No       | false                     | Autoplays the video as soon as it's loaded
loop                  | bool     | No       | false                     | Allows the video to continuously loop
title                 | string   | No       | ''                        | Adds a title of your video at the top of the player
placeholder           | string   | No       | undefined                 | Adds an image placeholder while it's loading and stopped at the beginning
logo                  | string   | No       | undefined                 | Adds an image logo at the top left corner of the video
theme                 | string   | No       | 'white'                   | Adds an optional theme colour to the players controls
hideFullScreenControl | bool     | No       | false                     | This hides the full screen control
style                 | number, object | No | {}                        | Apply styles directly to the Video player (ignored in fullscreen mode)
resizeMode            | string   | No       | 'contain'                 | Fills the whole screen at aspect ratio. contain, cover etc
rotateToFullScreen    | bool     | No       | false                     | Tapping the fullscreen button will rotate the screen. Also rotating the screen will automatically switch to fullscreen mode
fullScreenOnly        | bool     | No       | false                     | This will play only in fullscreen mode
inlineOnly            | bool     | No       | false                     | This hides the fullscreen button and only plays the video in inline mode
playInBackground      | bool     | No       | false                     | Audio continues to play when app enters background.
playWhenInactive      | bool     | No       | false                     | [iOS] Video continues to play when control or notification center are shown.
rate                  | number   | No       | 1                         | Adjusts the speed of the video. 0 = stopped, 1.0 = normal
volume                | number   | No       | 1                         | Adjusts the volume of the video. 0 = mute, 1.0 = full volume
onMorePress           | function | No       | undefined                 | Adds an action button at the top right of the player. Use this callback function for your own use. e.g share link
onFullScreen          | function | No       | (value) => {}             | Returns the fullscreen status whenever it toggles. Useful for situations like react navigation.
onTimedMetadata       | function | No       | undefined                 | Callback when the stream receives metadata
scrollBounce          | bool     | No       | false                     | Enables the bounce effect for the ScrollView
lockPortraitOnFsExit  | bool     | No       | false                     | Keep Portrait mode locked after Exiting from Fullscreen mode
lockRatio             | number   | No       | undefined                 | Force a specific ratio to the Video player. e.g. lockRatio={16 / 9}
onLoad                | function | No       | (data) => {}              | Returns data once video is loaded
onProgress            | function | No       | (progress) => {}          | Returns progress data
onEnd                 | function | No       | () => {}                  | Invoked when video finishes playing  
onError               | function | No       | (error) => {}             | Returns an error message argument
onPlay                | function | No       | (playing) => {}           | Returns a boolean during playback
error                 | boolean, object | No | true                     | Pass in an object to Alert. See https://facebook.github.io/react-native/docs/alert.html
theme                 | object   | No       | all white                 | Pass in an object to theme. (See example below to see the full list of available settings)
controlDuration             | number   | No       | 3                 | Set the visibility time of the pause button and the progress bar after the video was started


# Issues

Avoid adding alignItems: 'center' to the container, it can cause fullscreen mode to disappear :D

## Example

```jsx
import React, { useState } from 'react'
import { StyleSheet, View } from 'react-native'
import Video from 'react-native-clwy-video-player'

function VideoScreen({ route, navigation }) {  
  const [fullscreen, setFullscreen] = React.useState(false)
  React.useEffect(() => {
    navigation.setOptions({ headerShown: !fullscreen })
  }, [fullscreen, navigation])
  
  const logo = 'logo.png'
  const image = 'image.png'
  const source = '1.mp4'   

  return (
     <View style={styles.container}>
        <Video
            url={source}
            autoPlay
            logo={logo}
            placeholder={image}
            hideFullScreenControl={false}
            onFullScreen={status => onFullScreen(status)}
            rotateToFullScreen
        />
    </View>
  )
}

const styles = StyleSheet.create({
  container: {
    backgroundColor: '#fff',
    flex: 1,
    justifyContent: 'center',
  },
})

export default VideoScreen
```

# To Do

- [ ] Option to use custom icons
- [ ] Support Immersive mode for Android
- [ ] improve multiple videos fullscreen support within a ScrollView
- [ ] investigate subtitle support
- [x] Support for iOS
- [x] Provide fullscreen support within a ScrollView
- [x] Customise specific components for better theming

---

**MIT Licensed**
