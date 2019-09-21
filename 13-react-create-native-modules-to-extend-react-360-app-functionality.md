# 11. Create Native Modules to extend React 360 app functionality

[Video Link](https://egghead.io/lessons/react-create-native-modules-to-extend-react-360-app-functionality)

We would like to have it when we click on a flag and travel to a different country the title in the browser says "Welcome to Spain", "Welcome To Italy" etc.

Inside of the ```<changeBackground>``` method we'll pass ```<name>```. Then we'll add ```<document.title>``` = ```<'Welcome to' + name>```

```javascript
changeBackground(panorama, name) {
  Environment.setBackgroundImage(asset(panorama))
  document.title = 'Welcome to ' + name
}
```
After you save it doesn't change we have a problem. In the console we get a message 'Document is not defined'. It's not defined because React 360 runs inside of a web worker and they dont have acces to the DOM.

To enhance our application to do something that requires the DOM, we need to implement our value on native module. Let's head to clients.js

Then ```<import>``` 'module' from 'react-360-web'. Then create a new class we'll called it 'TitleChanger'. TitleChanger needs to extend the 'module' that we're importing from React 360.

```javascript
import { ReactInstance, Location, Surface, Module } from "react-360-web"

class TitleChanger extends Module {}
````
We need to make a c```<contructor>``` inside of the ```<TitleChanger>``` class. Then we create a ```<super>``` and pass in ```<TitleChanger>``` to it. Whatever is specified here is going to exposed to React 360.

```javascript
import { ReactInstance, Location, Surface, Module } from "react-360-web"

class TitleChanger extends Module {
  constructor() {
    super('TitleChanger')
  }
 ```
We'll then make a new method called 'changeTitle'. It will take 'title' as a parameter inside the method we'll add ```<document.title = title>```.

```javascript
changeTitle(title) {
  document.title = 'Welcome to ' + title
}
```
Next thing we need to do is expose the native module to our React code. to do that, when we are creating a new React 360 instanc, we can pass in custom options. So we'll pass in ```<nativeModules>```. It takes an array, we'll place ```<new TitleChanger>``` inside the array.

```javascript
function init(bundle, parent, options = {}) {
  const r360 = new ReactInstance(bundle, parent, {
    // Add custom options here
    fullScreen: true,
    nativeModules: [new TitleChanger()],
    ...options
  })
  ```

 After we save go back to index.js and import 'NativeModules' from 'react-360'. We need to get the title changer module from the native modules. Let's add '<const {TitleChanger} = NativeModules>' to get the title changer module.

```javascript
const { TitleChanger } = NativeModule
````
Now we need to delete our ```<document.title>``` from earlier and replace it with ```<TitleChanger.changeTitle('Welcome to ' + name)>```

```javascript
changeBackground(panorama, name) {
  Environment.setBackgroundImage(asset(panorama))
  TitleChanger.changeTitle('Welcome to ' + name)
}
```` 

Now if we click on the flags it will say Welcome to the countres name in the tabs on your browser.



## Personal Take:
I like how this lesson showed that React 360 couldn't access the DOM instead of going staight into using Native Modules it's good for a beginner to see both sides.


# Resources
[React 360 Native Modules Docs](https://facebook.github.io/react-360/docs/native-modules.html)
