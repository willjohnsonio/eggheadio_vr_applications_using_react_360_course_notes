# 05. Display images using the Image component in React 360

[Video Link](https://egghead.io/lessons/react-display-images-using-the-image-component-in-react-360)

The first thing we need to do, in order to display an image is ```import``` image from ```react-360``` 

```javascript
import React from "react"
import { AppRegistry, StyleSheet, View, Image } from "react-360"
```
Then we need to remove the ```<Text>``` component as well as the ```text``` styles that are inside of StyleSheet.create and replace ```text``` with a ```flag``` object. Now lets define some styles for ```flag```. We'll set the width to 50% and height to 40%

```javascript
const styles = StyleSheet.create({
  mainView: {
    width: 600,
    height: 600,
    padding: 10,
    backgroundColor: '#eee',
    alignItems: 'center',
  };
  flag: {
    width: '50%',
    height: '40%'
  }
})
```

Images can be displayed from the internet or from our ```static_assets``` folder in our project. To add our image we need to add ```style``` to our ```<Image>``` component and set the style to ```flag```. Next we add ```source``` to our ```<Image>``` component and set it to an object with a url property and a url for our image as the value. Save & refresh and an image wil be displayed on the screen.

```javascript
return (
  <View style={mainView}>
    <Image
      style={flag}
      source={{
        url: 'https://upload.wikimedia.org/wikipedia/commons/5/5a/Flag_of_Poland.jpg'
      }}
    />
  </View>
```

That is how we add and image using images externally, if we add an images from our own assets, we need to look into our projects files. All React 360 projects have a staic_assets folder.
To use assets in the folder we need to ```import``` asset from ```react-360```

```javascript
import React from "react"
import { AppRegistry, asset, StyleSheet, View, Image } from "react-360"
```

Then create another ```<Image>``` component. Set the style to flag as well and add source and set the url property to ```asset(flag_italy.png)``` 

```javascript
return (
  <View style={mainView}>
    <Image
      style={flag}
      source={{
        url:
          'https://upload.wikimedia.org/wikipedia/commons/5/5a/Flag_of_Poland.jpg'
      }}
    />
    <Image style={flag} source={asset('flag_italy.png')} />
  </View>
```

The ```asset``` function looks inside of the assets directory and grabs the flag_italy.png for us(which is a lot easier than using using the filepath).


Save & refresh and now we should have two ```<Image>``` components with two flags displayed from two different sources.


## Personal Take:
I'm really impressed by the amount action he puts into his lessons in such a short time. This lesson was straight forward and nothing was hard to understand for me.


# Resources
[React 360 Docs Image Component](https://facebook.github.io/react-360/docs/image.html)
