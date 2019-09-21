# 12. Add animations to React 360 componentsty

[Video Link](https://egghead.io/lessons/react-add-animations-to-react-360-components)

In this updated version of our app with have our Earth component up here. Let's animate it by making it bounce up and down while spinning. First, we will import ```<Animated>``` from 'react-360'

```javascript
import React from "react"
import { Animated, asset, View } from "react-360"
import Entity from "Entity"
import AmbientLight from "AmbientLight"
import PointLight from "PointLight"
```

Now, we'll create a new ```<AnimatedEntity>``` component. We'll wrap the Entity Component inside of an animated library component imported from React 360.

```javascript
const AnimatedEntity = Animated.createAnimatedComponent(Entity)
```
Replace our ```<Entity>``` component with ```<AnimatedEntity>```.

```javascript
<AnimatedEntity
  source={{ gltf2: asset("Earth.gltf") }}
  style={{
    transform: [
      { translateY: this.jumpValue },
      { scale: 0.001 },
      { rotateY: this.rotation }
    ]
  }}
/>
```
Next create a new animated value. Let's create a rotation value and set it to ```new Animated.Value(0);```

```javascript
export default class Earth extends React.Component {
  rotation = new Animated.Value(0);
```
Then we'll create a spin function. Inside of this function set the rotation value to 0. Next, we'll add the  ```<Animated.timing>``` function to modify the rotation value from 0 to 360. Add in ```<this.rotation>``` and provide an object with options inside of it.

First, set the rotation value to 360 with a duration of 4 seconds. Then call the ```<.start()>``` fuuntion which takes a callback. Inside the callback will we have the rotation start again. To create an infinite rotation.

```javascript
spin() {
  this.rotation.setValue(0);
  Animated.timing(this.rotation, {
    toValue: 360,
    duration: 4000,
  }).start(() => this.spin())
}
```
Under the spin function we will add a ```<ComponentDidMount>``` function inside of it run ```<this.spin>```

```javascript
componentDidMount() {
  this.spin()
```

To use the spin value set it to the rotateY value. Set it to ```<this.rotation>```

```javascript
<AnimatedEntity
  source={{ gltf2: asset("Earth.gltf") }}
  style={{
    transform: [
      { translateY: this.jumpValue },
      { scale: 0.001 },
      { rotateY: this.rotation }
    ]
  }}
/>
```

Now we have spin earth model! As you can see it slows down in the middle of the rotation then speeds up. That happens because the animated timing function is using an in and out easing function. Which means that both the beginning and the end of the animation is slower.

To fix that we can import ```<Easing>``` from ```<Easing>``` and set ```<easing>``` to ```<Easing.linear>```

```javascript
import React from "react"
import { Animated, asset, View } from "react-360"
import Entity from "Entity"
import Easing from "Easing"
import AmbientLight from "AmbientLight"
import PointLight from "PointLight"

const AnimatedEntity = Animated.createAnimatedComponent(Entity);

export default class Earth extends React.Component {
  rotation = new Animated.Value(0)

  spin() {
  this.rotation.setValue(0);
  Animated.timing(this.rotation, {
    toValue: 360,
    duration: 4000,
    easing: Easing.linear
  }).start(() => this.spin())
}

componentDidMount() {
  this.spin()
```

Now the speed is consistent and doesn't slow down. Now we want to make our Earth jump up and down. 

First, we'll create two new variables ```<LOW_JUMP_VALUE>``` and ```<TOP_JUMP_VALUE>```. Inside of our Earth component we will add a new ```<jumpValue>``` and set to to ```<new Animated.Value()>``` and the default value we'll set to ```<LOW_JUMP_VALUE>```

```javascript
const AnimatedEntity = Animated.createAnimatedComponent(Entity)
const LOW_JUMP_VALUE = 1.5
const TOP_JUMP_VALUE = 1.75

export default class Earth extends React.Component {
  rotation = new Animated.Value(0)
  jumpValue = new Animated.Value(LOW_JUMP_VALUE)

  spin() {
    this.rotation.setValue(0)
    Animated.timing(this.rotation, {
      toValue: 360,
      duration: 4000,
      easing: Easing.linear
    }).start(() => this.spin())
    }
```

Now add a junp function it will take the current value as an argument. Then we'll create a new variable called ```<nextValue>``` which is going to be whatever the currentValue is if it's ```<TOP_JUMP_VALUE>``` it'll be replaced by ```<LOW_JUMP_VALUE>```. In the other case it'll be ```<TOP_JUMP_VALUE>```.

```javascript
jump(currentvalue) {
  let nextValue = currentValue === TOP_JUMP_VALUE ? LOW_JUMP_VALUE : TOP_JUMP_VALUE
```
Let's use the ```<Animated.timing>``` function to modify ```<this.jumpValue>```. 


Change ```<this.jumpValue>``` toValue of nextValue set it to half a second. Call .start(),  and provide a callback, and call the jump function with the nextValue.

```javascript
jump(currentvalue) {
  let nextValue = currentValue === TOP_JUMP_VALUE ? LOW_JUMP_VALUE : TOP_JUMP_VALUE

  Animated.timing(this.jumpValue, {
    toValue: nextValue,
    duration: 500
  }).start(() => this.jump(nextValue))
}
```
Then we're going to call it in the componentDidMount. Add ```<this.jump>```and I'm going to pass in ```<LOW_JUMP_VALUE>``` as a parameter.

```javascript
componentDidMount() {
  this.spin()
  this.jump(LOW_JUMP_VALUE)
}
```
We'll use ```<this.jumpValue>``` in the translate Y. I'm going to replace that 1.5 with ```<this.jumpValue>```. Save and refresh.

```javascript
<AnimatedEntity
  source={{ gltf2: asset('Earth.gltf') }}
  style={{
    transform: [
      { translateY: this.jumpValue },
      { scale: 0.001 },
      { rotateY: this.rotation }
      ]
```

Now we see both animation running at the same time spinning and jumping!



## Personal Take:
this was a really good lessons showed you how easy it is to add animations to React 360 apps without knowing a lot about animations.


# Resources
[React Native Animated Library Docs](http://facebook.github.io/react-native/docs/animated.html)