[Video Link](https://egghead.io/lessons/react-create-a-flat-surface-and-attach-a-component-to-it-in-react-360)

# 07. Create a Flat Surface and attach a component to it in React 360

The second type of surface in React 360 is a flat surface. We're going to use the flat surface to make a ```<Flag>``` component and display it on a flat surface.

We want to make a new components directory and create a flag.js file inside of the directory. Then we'll ```<import>``` 'React' from 'react' and ```<import>``` 'asset, StyleSheet, and Image from 'react 360'

```javascript
import React from "react"
import { asset, StyleSheet, Image } from "react-360"
```
Create a new class and name it 'Flag' and extended it from ```<React.component>```. Inside of that we will desturcture flag from styles, then ```<render>``` an ```<Image>```. We will set the style to flag, and set the source to what is provided by the props.

```javascript
export default class Flag extends React.Component {
  render() {
    const { flag } = styles

    return <Image style={flag} source={asset(this.props.image)} />
  }
}
```
Now let's create a ```StyleSheet``` object. Let's set flag's height to 400 and width to 600. 

```javascript
const styles = StyleSheet.create({
  flag: {
    height: 400,
    width: 600
  }
})
```
To attach a React component to a Surface, it must be registered with the AppRegistry.

Go to index.js here we can see the ```<travelVR>``` component has been registered, and can be ued in client.js where our runtime lives. We need to register our flag component by copying the ```<travelVR>``` Registry and change it to ```<Flag>```  and import it to. 

Import Flag from ./components/Flag

```javascript
import React from "react"
import { AppRegistry, asset, StyleSheet, View, Image } from "react-360"
import Flag from "./components/Flag"

export default class travelVR extends React.Component {
  render() {
    const { mainView } = styles

    return <View style={mainView} />
  }
}

const styles = StyleSheet.create({
  mainView: {
    width: 4680,
    height: 600,
    opacity: 0.3,
    backgroundColor: "#eee",
    alignItems: "center"
  }
})

AppRegistry.registerComponent("travelVR", () => travelVR)
AppRegistry.registerComponent("Flag", () => Flag)
```

Save it then open clients.js. Create a new flat surface ```<const myFlatSurface>``` set it to ```<new Surface>``` 600 by 400 and the ```<Surface.SurfaceShape.Flat>```

```javascript
const mySurface = new Surface(4680, 600, Surface.SurfaceShape.Cylinder)
```

Next we need to render a componet to ```<myFlatSurface>```

```javascript
const myFlatSurface = new Surface(600, 400, Surface.SurfaceShape.Flat)
r360.renderToSurface(
  r360.createRoot("Flag", {
    /* initial props */
  }),
  myFlatSurface
)
```

Now we pass props to the ```<Flag>``` Let's pass an ```<image>`` prop and set it to flag.italy.png

```javascript
const myFlatSurface = new Surface(600, 400, Surface.SurfaceShape.Flat)
r360.renderToSurface(
  r360.createRoot("Flag", {
    image: "flag_italy.png"
  }),
  myFlatSurface
)
```
If we want to set the flag on our screen we need to specify what angle it to display on the flat surface. We need to set ```<myFlatSurface.setAngle()>```. This function takes two arguements, how much to rotate the surface let and right and up and down. Can be set by either radians or degrees. 

First radians ```<Math.PI>``` / 4 and the seceond number (pitch angle) will be 0.

```javascript
const myFlatSurface = new Surface(600, 400, Surface.SurfaceShape.Flat)
myFlatSurface.setAngle(Math.PI / 4, 0)
```
To make it easiter we'll use the number 45 for 45 aegress instead ```<Math.PI>``` / 4. The second number stays 0. It will have the smae outcome.

```javascript
const myFlatSurface = new Surface(600, 400, Surface.SurfaceShape.Flat)
myFlatSurface.setAngle(45 / 0)
```

The big difference between a flat surface and a cylinder is that the flat surface is not curved. 


# Personal Take
This lesson on my first watch seemed kinda of fast especially when switching to different files and when registering a new component. Those two parts could have been slower or explain a little bit more.









# Resources

[React 360 Docs Surfaces Docs](https://facebook.github.io/react-native/docs/style)



