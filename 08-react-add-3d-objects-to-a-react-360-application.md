[Video Link]https://egghead.io/lessons/react-add-3d-objects-to-a-react-360-application)

# 08. Add 3D objects to a React 360 application

React 360 applications are not restricted to 2D panels in space – you can also bring in 3D elements.

To import a 3D model in React 360, go componets and create a files called earth.js. Then import React from 'react`
and import asset and view from 'react-360'

```javascript
import React from "react"
import { asset, View } from "react-360"
```
You can use the ```<Entity>``` component to bring your 3D model in your project. Create a new components ours will be called earth and it will extend React.component and render a ```<View>``` component inside of it then ```<Entity>``` inside of ```<View>```

Entity is what allows us to bring in 3D models. You can either design something ot use a website like Google Poly and download a free models. 

React 360 accepts the OBJ and GLTF2 file type.Put the file you downloaded into static_assets.```<Entity>``` has a source attribute we're going have it take an object gltf2 and set ti equal to Earth.gltf

```javascript
export default class Earth extends React.Component {
  render() {
    return (
      <View>
        <Entity source={{ gltf2: asset('Earth.gltf') }}/>
      </View>
```
In the index.js files we need to register and import the Earth componet

```javascript
import React from "react"
import { AppRegistry, asset, StyleSheet, View, Image } from "react-360"
import Flag from "./components/Flag"
import Earth from "./components/Earth"

export default class travelVR extends React.Component {
  render() {
    const { flagContainer } = styles

    return <View style={mainView} />
  }
}

const styles = StyleSheet.create({
  flagContainer: {
    height: 600,
    width: 4680,
    backgroundColor: "rgba(255, 255, 255, 0.3)",
    flexDirection: "row",
    alignItems: "center",
    justifyContent: "center"
  }
})

AppRegistry.registerComponent("travelVR", () => travelVR)
AppRegistry.registerComponent("Flag", () => Flag)
AppRegistry.registerComponent("Earth", () => Earth)
```
We can't use a surface to render this component. Surfaces are for displaying React componets to flat planes on a cylinder or flat surface.

We need to use ```<Location>``` to render the 3D Object. First thing we do is import 'location' from 'react-360' and create a new Location and name it myNewLocation and assign it to ```<new Location()>``` inside of the ```<()>``` place an array telling the position of the new location within the x, y and z axis. We'll set it as 3 meters, for the x axis, 0 meters for the y axis and negative 1 meter for the z axis.


Inside client.js we'll render the earth component to the ```<new Location>```. So we'll type in ```<r360.RenderToLocation>```. Then we'll create a new root ```<r360.createRoot>```, with the ```<Earth>``` component. 

```javascript
const myNewLocation = new Location([3, 0, -1])
r360.renderToLocation(r360.createRoot("Earth"), myNewLocation)
```

Now we need to add some light. THere are different types of lighting avalible in React 360. Today we'll use ```<AmbientLight>```, to use it we have to import it from ```<AmbientLight>``` 

```javascript
import AmbientLight from "AmbientLight"
```

We'll set the intensity to 1.0, and the color to white.

```javascript
<AmbientLight intensity={1.0} color={'#fff'} />
```

Now the earth is HUGE! We need to resize it! To change the size we need to use the ```<transform>``` property. We need to add a ```<style>``` attribute inside of the style we add our transform. We'll set the ```<scale>``` to 0.003, ```<rotateY>``` by 120 degrees and ```<rotateX>``` -30 degrees.

```javascript
export default class Earth extends React.Component {
  render() {
    return (
      <View>
        <AmbientLight intensity={1.0} color={'#fff'} />
        <Entity
        source={{ gltf2: asset('Earth.gltf') }}
        style={{
          transform: [
            { scale: 0.003 },
            { rotateY: 120 },
            { roateX: -30 }
          ]
          }}
        />
      </View>
```

Now you see the texture on our object is flat. Thats because the ```<AmbientLight>``` we're using has the same intensity in all directions. To show our the shadows on our Earth object we need to import ```<PointLight>```  from ```<PointLight>```

```javascript
import PointLight from "PointLight"
```

Add the same intensity and color, but we need to transform it. Add ```<style>``` to ```<PointLight>``` and add the transform property, then ```<translate>``` which means move our light source to [0,0,20]. 

```javascript
<View>
  <AmbientLight intensity={1.0} color={"#fff"} />
  <PointLight
    intensity={1.0}
    color={"#fff"}
    style={{
      transform: [{ translate: [0, 0, 20] }]
    }}
  />
  <Entity
    source={{ gltf2: asset("Earth.gltf") }}
    style={{
      transform: [{ scale: 0.003 }, { rotateY: 120 }, { roateX: -30 }]
    }}
  />
</View>
```





# Personal Take
The point light was the highlight of this lesson for me. It was so simple to do and it showed me the power React 360 has built in. I was really impressed with that.

# Resources
[React 360 3D Objects Docs](https://facebook.github.io/react-360/docs/objects.html)



