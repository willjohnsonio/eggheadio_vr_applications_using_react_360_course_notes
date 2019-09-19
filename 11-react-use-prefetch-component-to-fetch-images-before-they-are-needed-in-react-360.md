# 11. Use Prefetch component to fetch images before they are needed in React 360

[Video Link](https://egghead.io/lessons/react-use-prefetch-component-to-fetch-images-before-they-are-needed-in-react-360)

Currently in our app when we click on a flag it will send a request to fetch the 360 panorama image(2.3MB). This can cause performance issues especially on mobile. 

It would be helpful to preload all the images in the background. So instead of clicking the button and sending the request the image will be already loaded.

First thing we need to do is we need to import ```<Prefetch>``` and ```<Fragment>``` from 'react-360'. 

```javascript
import {
  AppRegistry,
  asset,
  StyleSheet,
  View,
  Prefetch,
  Image,
  Environment,
  VrButton
} from "react-360"
import Flag from "./components/Flag"
import Earth from "./components/Earth"

```

Then in the ```<renderFlags()>``` method, we'll place ```<VrButton>``` inside of a ```<Fragment>```. The place the ```<Prefetch>``` componment inside of Fragment as well.

```<Prefetch>``` takes a source we'll set the source to be ```asset(panorama)```. So that when all of the places are being rendered their correspnding panorama is being fetched and preloaded for later.

```javascript
renderFlags() {
  return PLACES.map(({ panorama, flag }) => (
    <Fragment key={flag}>
      <Prefetch source={asset(panorama)} />
      <VrButton
        onEnter={() => this.setState({ activeFlag: flag })}
        onExit={() => this.setState({ activeFlag: '' })}
        onClick={() => this.changeBackground(panorama)}
      >
        <Flag image={flag} activeFlag={this.state.activeFlag} />
      </VrButton>
    </Fragment>
  })
}
````
Since the images will be preloaded the app will have better preceived performance.



## Personal Take:
Even though the prefetch component was easy to understand but for whatever reason I couldn't find any information on it. Other than that this was a great to the point lesson.


# Resources
N/A