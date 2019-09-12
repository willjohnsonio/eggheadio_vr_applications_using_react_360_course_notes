[Video Link](https://egghead.io/lessons/react-write-text-using-the-react-360-text-component)

# 02. Write text using the React 360 Text component

To write our own text and style we need to remove the boilerplate from the ```travelVR``` component (have it return null;) and any default styles from ```StyleSheet.create```


```javascript
export default class travelVR extends React.Component {
  render() {
    return null;
  }
}

const styles = StyleSheet.create({});
```

Then create a ```<View>``` component inside of the ```travelVR``` component. Inside of ```<View>``` add a ```<Text>``` component. Inside you ```<Text>``` type in Hello Egghead

Save & Refresh to see your new text

```javascript
export default class travelVR extends React.Component {
  render() {
    return (
      <View>
        <Text>Hello Egghead</Text>
      </View>
    )
  }
}
```

So we can style both ```<View>``` (which is like a div) and ```<Text>``` we can go inside of the StyleSheet.create and create ```mainView``` and ```greetings``` objects and set style inside of them like this.


```javascript
const styles = StyleSheet.create({
  mainView: {
    height: 600,
    width: 600,
    padding: 10,
    backgroundColor: "#eee"
  },
  greetings: {
    fontSize: 40,
    width: "50%",
    marginTop: 5,
    backgroundColor: "#0298D0",
    color: "white"
  }
})
```

React component takes a ```style``` property. We can our ```<View>``` component by adding style and setting equal to ```styles.mainView``` that will make our ```<View>``` container take on the styles we set. We style the text by add ```style``` to the ```<Text>``` component and make it equal to ```styles.greetings```.

```javascript
	export default class travelVR extends React.Component {
  render() {
    return (
      <View style={styles.mainView}>
        <Text Style={styles.greetings}>Hello Egghead</Text>
      </View>
    )
  }
}
```

Save & refresh and we should see our new styles that we defined. We can use use the same styles on more than one component. If we add another ```<Text>``` component and just change the text to 'Hello Again' 

```javascript
	export default class travelVR extends React.Component {
  render() {
    return (
      <View style={styles.mainView}>
        <Text Style={styles.greetings}>Hello Egghead</Text>
        <Text Style={styles.greetings}>Hello Again</Text>
      </View>
    )
  }
}
```


Save & refresh and now we should have two ```<View>``` components with the exact same styles.


## Personal Take:
I really like how this lesson was focused on action, we made a lot of changes and it was easy to grasp. I feel like it was effective in helping me be confident to re-create these steps on my own and understand what i doing
