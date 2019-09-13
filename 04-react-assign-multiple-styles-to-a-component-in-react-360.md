[Video Link](https://egghead.io/lessons/react-assign-multiple-styles-to-a-component-in-react-360)

# 04. Assign multiple styles to a component in React 360

Now we have our ```<View>``` component with a list of countries that we want to visit. Also, in ```StyleSheet.create``` we have a country object for each country on our list. Inside the objects we have a background color defined as a color that comes from the flag of each country in our list. We want to apply the color property to each country in our list.

We're going to destructure all the styles from ```styles`` object

```javascript
const { mainView, menuItem, poland, ukraine, uk, spain, italy, greece } = styles
```
Then, we will remove the ```styles``` from ```style.menuItem``` and the country names are still displayed.

```javascript
const { mainView, menuItem, poland, ukraine, uk, spain, italy, greece } = styles
return (
  <View style={styles.mainView}>
    <Text style={menuItem}>Poland</Text>
    <Text style={menuItem}>Ukraine</Text>
    <Text style={menuItem}>Great Britain</Text>
    <Text style={menuItem}>Spain</Text>
    <Text style={menuItem}>Italy</Text>
    <Text style={menuItem}>Greece</Text>
  </View>
)
```
For us to provide multiple styles for the ```<Text>``` components, we need to pass in an array of styles to the ```style``` property. Wrap all the styles into an array using brackets[]. Place ```menuItem``` followed by a comma then the country name that was destructured. Then save & refresh

```javascript
return (
  <View style={styles.mainView}>
    <Text style={[menuItem, poland]}>Poland</Text>
    <Text style={[menuItem, ukraine]}>Ukraine</Text>
    <Text style={[menuItem, uk]}>Great Britain</Text>
    <Text style={[menuItem, spain]}>Spain</Text>
    <Text style={[menuItem, italy]}>Italy</Text>
    <Text style={[menuItem, greece]}>Greece</Text>
  </View>
)
```

Now each ```<Text>``` component we made is set a with the backgroundColor property from the country's name object.

To add new styles create a new ```redtext``` object inside of the ```menuItem``` object and set the color to red.

```javascript
redText: {
  color: 'red'
}
```
If we want to display this color on the component with the Italy styles. We add a comma after Italy then type ```redText``` after. Also make sure ```redText``` is destuctured from ```styles``` as well.
After a save & refresh Italy should now have red text.

```javascript
const {
  mainView,
  menuItem,
  poland,
  ukraine,
  uk,
  spain,
  italy,
  greece,
  redText
} = styles
return (
  <View style={styles.mainView}>
    <Text style={[menuItem, poland]}>Poland</Text>
    <Text style={[menuItem, ukraine]}>Ukraine</Text>
    <Text style={[menuItem, uk]}>Great Britain</Text>
    <Text style={[menuItem, spain]}>Spain</Text>
    <Text style={[menuItem, italy, redText]}>Italy</Text>
    <Text style={[menuItem, greece]}>Greece</Text>
  </View>
)
```


# Personal Take
I felt like this one kinda of fast, and I ofund myself trying to play catch up. In the previous lessons I had no issues understanding and implementing. I feel maybe going a little slower or into a little more detail about how styling is working









# Resources

[React Native Docs Style](https://facebook.github.io/react-native/docs/style)



