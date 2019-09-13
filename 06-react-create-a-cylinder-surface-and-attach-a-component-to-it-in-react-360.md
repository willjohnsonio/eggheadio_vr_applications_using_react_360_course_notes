# 06. Create a Cylinder Surface and attach a component to it in React 360

[Video Link](https://egghead.io/lessons/react-create-a-cylinder-surface-and-attach-a-component-to-it-in-react-360)

We have been creating and editing components inside of an index.js file. There is also a second JavaScript file thats get created automatcially when you strart a new React 360 project. This file is named clients.js it's referred as the runtime because its where your React code in initialized.

Let's focus on ```r360.renderToSurface()``` we're rendering our ```travelVR``` component we have been working on in index.js. Right now we're using ```DefaultSurface```.

React 360 has two different type of surfaces. A cylinder surface and a flat surface. We'll look at cylinder becuase it it's what we have been working on so far.

The top and bottom of component is curved because it's currently been projected onto a cylinder. The cylinder is a sphere of a four meter raduius that is surronding the users view.

We are able to project differnet components on top of the surface like our ```travelVR``` component. 

We can also use our own surface instead of the default one. First step is to ```import``` surface from ```react-360-web``` into cliens.js

```javascript
import { ReactInstance, Location, Surface } from "react-360-web"
```
Then we'll create a new surface name it ```mySurface``` then assign it to ```new Surface()```. Inside of the () let's set the width to 4680. height to 600 and set Surface.SurfaceShape.Cylinder.   

```javascript
const mySurface = new Surface(4680, 600, Surface.SurfaceShape.Cylinder)
```

We set the width to 4680 because that's going to create a surface that's going to wrap around the user view completly 360 degrees

To have the new surface show up on the screen we're going to remove the defauly surface and replace it with our newly created ```mySurface```

```javascript
const mySurface = new Surface(4680, 600, Surface.SurfaceShape.Cylinder)

// Render your app content to the default cylinder surface
r360.renderToSurface(
  r360.createRoot("travelVR", {
    /* initial props */
  }),
  mySurface
)
```

Now if we rotate our view we can see the component, the component moves to the begining of the surface. Now we're going to create a component that we can see in front of our view no matter which way we look.

Go back to index.js. Remove both flags from our ```<View>``` component, also remove flags from StyleSheet.create, and from the destuectured styles inside of Reaact.component. Change the width of ```mainView``` from 1000 to 4680(so it can match the width of the cylinder). Then add opcaity and set it to 0.5.

```javascript
const styles = StyleSheet.create({
  mainView: {
    width: 4680,
    height: 600,
    opacity: 0.3,
    backgroundColor: "#eee",
    alignItems: "center"
  }
})
```

## Personal Take:
We made a lot of changes and introduce some new things like client.js and the different surfaces still didn't feel like it was moving too fast. Even when i check the docs to find any gotchas it's usually mentioned great content.


# Resources
[React 360 Docs Surfaces](https://facebook.github.io/react-360/docs/surfaces.html)