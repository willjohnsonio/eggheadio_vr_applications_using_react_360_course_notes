[Video Link](https://egghead.io/lessons/react-change-360-panorama-background-in-react-360-app)

# 10. Change 360 panorama background in React 360 app

We can change the background in a few different places. First place is inside of cilent.js. We can change the background inside of ```<r360.compositor.setBackground>```, Right now it is set to ```<360_world.jpg>```. We can change it to ```spain.jpg```, it will now change the background to this picture of Spain.

```javascript
// Load the initial environment
r360.compositor.setBackground(r360.getAssetURL('spain.jpg'))
}

window.React360 = { init }
```
This picture is in our static_assets folder. We can change the background dynamically as well.

Open up index.js. Each object in the PLACES array has a flag and panorama associtated with it. Spain for example has a flag of Spain and a panorama image.

```javascript
{
    flag: 'flag_spain.png',
    panorma: 'spain.jpg'
}
```
In the ```<renderFlags()>``` method we are mapping over all the objects in the PLACES array and display the flag for each country. Now we want the background to change whenever a user clicks one of those flags, like they are traveling to that place.

First step is to import ```<Environment>``` from 'react-360`

```javascript
import React, { Fragment } from "react"
import {
  AppRegistry,
  asset,
  StyleSheet,
  View,
  Image,
  Environment,
  VrButton
} from "react-360"
import Flag from "./components/Flag"
import Earth from "./components/Earth"
```

Now let's create a ```changeBackground``` method. It's going to take the ```panorama`` as an argument. Then inside of the method we going put ```<Environment.setBackgroundImage>```. We'll used the asset function to get the image associated with the panorama.

```javascript
export default class travelVR extends React.Component {
  state = {
    activeFlag: ''
  };

  changeBackground(panorama) {
    Environment.setBackgroundImage(asset(panorama));
  }
```

On our ```<onClick>``` handler. We'll call ```<this.changeBackground(panorama)>```

```javscript
renderFlags() {
  return PLACES.map(({panorama, flag }) => (
    <VrButton
      onClick={() => this.changeBackground(panorama)}
      onEnter={() => this.setState({ activeFlag: flag })}
      onExit={() => this.setState({ activeFlag: '' })}
    >
```

Now when we click on the our different flags the background image will change







# Personal Take
Nothing really this course get more clear and concise as it moves on

# Resources
[React 360 Environment Docs](https://facebook.github.io/react-360/docs/environment.html)

[React 360 Docs on 360 Photos and Videos](https://facebook.github.io/react-360/docs/photos-and-videos.html)
