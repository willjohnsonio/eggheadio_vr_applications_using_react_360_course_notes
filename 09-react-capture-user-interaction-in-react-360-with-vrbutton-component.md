[Video Link](https://egghead.io/lessons/react-capture-user-interaction-in-react-360-with-vrbutton-component)

# 09. Capture user interaction in React 360 with VrButton component

This version of the app has been updated to include more flags. At this point our app is static, we aren't able do anything with this app besides look at it. 

To add some interactivity to our app, we need to import ```<VrButton>``` from 'react-360`

```javascript
import React from "react"
import {
  AppRegistry,
  asset,
  StyleSheet,
  View,
  Image,
  VrButton
} from "react-360"
import Flag from "./components/Flag"
import Earth from "./components/Earth"
```

Then we'll put our ```<Flag>``` component inside of our ```<VrButton>```. Also, lets move the key to the ```<VrButton>``` 

```javascript
export default class travelVR extends React.Component {
  renderFlags() {
    return FLAGS_IMAGES.map(image => (
      <VrButton key={image}>
        <Flag image={image} />
      </VrButton>
    ))
```
Add an ```<onClick>```,```<onEnter```,```<onExit>``` . They'll take a function.

Hovering on the flag is onEnter, moving your mouse away from the flag is onExit. Clicking on the flag of course is onClick.

```javascript
export default class travelVR extends React.Component {
  renderFlags() {
    return FLAGS_IMAGES.map(image => (
      <VrButton
        key={image}>
        onClick={() => console.log('Click')}
        onEnter={() => console.log('Enter')}
        onExit={() => console.log('Exit')}
      >
        <Flag image={image} />
      </VrButton>
    ))
```

**Also to note when using VrButton onEnter and onExit behave differently based on the device. Looking at the flag would be onEnter and looking way would be onExit**

Let's head to our Flag.js component and make the opacity: 0.7.

```javascript
const styles = StyleSheet.create({
  flag: {
    height: 400,
    width: 600,
    marginRight: 20,
    opacity: 0.7
  }
```

The default for our flags is inactive. Let's add active and set the opacity to 1. Destructure active from styles and destructure ```<image>``` and ```<activeFlag>``` from ```<this.props>```. The we'll mosdify the style prop.

Pass in the ```<flag>``` prop and when activeFlage to equal to the current image, we're going to apply our ```<active>``` styles with it.

```javascript
export default class Flag extends React.Component {
  render() {
    const { flag, active } = styles
    const { image, activeFlag } = this.props

    return (
      <Image
        style={[flag, activeFlag === image && active]}
        source={asset(this.props.image)}
      />
    )
  }
}
```

Now let's head back to index.js in this file we will add some state. Let's start by setting ```<activeFlag>``` as an empty string. We're going to change it using the ```<onEnter>``` handler. Set it to ```<this.setState>```, and have the ```<activeFlag>``` set to current image.

```javascript
renderFlags() {
  return FLAGS_IMAGES.map(image => (
    <VrButton
      key={image}
      onClick={() => console.log('Click')}
      onEnter={() => this.setState({ activeFlag: image})}
      onExit={() => console.log({'Exit')}
    >
      <Flag image={image}  />
    </VrButton>
  ));
}
```
Next let's do something similar to our onExit handler. We'll just reset the ```<activeFlag>``` to an empty string. 

```javascript
onExit={() => this.setState({ activeFlag: '' })}
```

We also need to pass in this active flag state to the flag component as well. We'' do this with setting ```<activeFlag>``` to ```<this.state.activeFlag>```.

```javascript
renderFlags() {
  return FLAGS_IMAGES.map(image => (
    <VrButton
      key={image}
      onClick={() => console.log('Click')}
      onEnter={() => this.setState({ activeFlag: image})}
      onExit={() => this.setState({ activeFlag: '' })}
    >
      <Flag image={image} activeFlag={this.state.activeFlag}/>
    </VrButton>
  ));
}
```

Now we can clearty see which flags are active when hovered.





# Personal Take
Another solid lessons nothing much differenrt to say. If you know React you should understand this course.

# Resources
[React 360 VrButton Docs](https://facebook.github.io/react-360/docs/vr-button.html)

[CSS Tricks understand React 'setState'](https://css-tricks.com/understanding-react-setstate/)
