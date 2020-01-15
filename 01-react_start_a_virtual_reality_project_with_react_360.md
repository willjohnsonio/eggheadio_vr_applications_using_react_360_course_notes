[Video Link](https://egghead.io/lessons/react-start-a-virtual-reality-project-with-react-360)

# 01. Start a Virtual Reality project with React 360

Get stated with React 360 by installing the React 360 CLI. Once the install has been completed use the `init` command to create a new project. We'll call this project `travelVR`

```npm install react-360-cli -g

   react-360 init travelVR
   ```

   Once the dependecies are done, go into the product directory used `cd` and the project name. Then run `npm start` to start the React Native Packager.

   ```cd TravelVR

   npm start
   ```

   Once that's done it will tell us to open our browser to a localhost URL (http://localhost:8081/index.html)

   After all the dependencies are loaded. You should have a 360 'Welcome to React 360 screen', that you can look around on.

   **The important thing to remember about React 360**
   
   Even though it runs in a VR environment, its not that different from the React we know on the web

   We have an index.html file. We have things like **React components**. Something from React Native called **View**. Also, we have the **StyleSheet** object so we can write CSS-in-JS in VR.


   To make sure everything is set up properly change the text from 'Welcome to React 360' to 'Welcome to egghead'. Save and refresh, if the text on the screen changes it's time to getting going and implement our app!

   ```
    <Text style={styles.greeting}>
    Welcome to EggHead
    </Text>

   ```




   **Resources**
   
   [Setting up Tools, and Creating Your First Project](https://facebook.github.io/react-360/docs/setup.html)

   [View in React Native](https://facebook.github.io/react-native/docs/view#docsNav)

   [StyleSheet](https://facebook.github.io/react-native/docs/stylesheet)

