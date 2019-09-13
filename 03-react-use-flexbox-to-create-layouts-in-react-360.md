[Video Link](https://egghead.io/lessons/react-use-flexbox-to-create-layouts-in-react-360)

# 03. Use flexbox to create layouts in React 360

We have two components displayed. We set their ```width``` to 30 percent inside of ```StyleSheet.create```. They're currently displayed on top of each other, even though they could fit on one line.

They're displayed this way by default because React 360 uses Flexbox for layouts.(That comes from React Native, React 360 borrows it's layout implementation from it). The default ```flexDirection``` is column. If we change the ```flexDirection``` of the ```mainView```component to row, the text components will now display on a single line. 

```javascript
const styles = StyleSheet.create({
  mainView: {
    height: 600,
    width: 600,
    padding: 10,
    backgroundColor: "#eee",
    flexDirection: "row"
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
Now were going to make a list of countries that we will visit in our Travel VR app. We'll paste in some text components with the countries. Next we're going to rename  ```greeting``` to ```menuItem``` and remove the the ```flexDirection``` that is set to row.

```javascript
<View style={styles.mainView}>
  <Text style={styles.menuItem}>Poland</Text>
  <Text style={styles.menuItem}>Ukraine</Text>
  <Text style={styles.menuItem}>Great Britain</Text>
  <Text style={styles.menuItem}>Spain</Text>
  <Text style={styles.menuItem}>Italy</Text>
  <Text style={styles.menuItem}>Greece</Text>
</View>
```

Save & refresh then we'll see all those countries displayed on the screen.

Also, lets remove the hard coded```height```. We're going to center the list of countries in the middle of the component. We're going to use Flexbox again. Inside of the ```mainView``` component, we'll add ```alignItems``` and set it to ```center``` then add ```justifyContent``` and set it to ```center``` as well. After you Save & refresh we will see the list of countries centered both horizontally and vertically inside of the ```mainView``` component.

```javascript
const styles = StyleSheet.create({
  mainView: {
    height: 600,
    width: 600,
    padding: 10,
    backgroundColor: "#eee",
    flexDirection: "row"
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


# Personal Take
Good on explaining where the use of flexbox comes from and show the difference between row and column. As someone who doesn't extensive React experience this was very approachable.









# Resources

[React 360 Docs Layout](https://facebook.github.io/react-360/docs/layout.html)


[React Native Docs Layout with Flexbox](http://facebook.github.io/react-native/docs/flexbox)

