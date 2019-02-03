# mapState Vue

The following was found in [Don’t understand how to use mapState from the docs](https://forum.vuejs.org/t/dont-understand-how-to-use-mapstate-from-the-docs/14454/11)
by [LinusBorg](https://forum.vuejs.org/u/LinusBorg)

given this state:

````
state: {
user: 'Tom',
age: 25
}
````

mapState returns an object with functions returning the given state:

````
mapState(['user', 'age'])
// returns:
{
  user () {
    return this.$store.state.user
  },
  age () {
    return this.$store.state.age
  }
}
````

Now, using the Object rest spread operator, we can insert this result into our computed properties::slight_smile:

````
computed: {
  ...mapState(['user', 'age']), // no semicolon - we are "in" an object, you can only use a comma.
  myOwnComputedProp() {  return whatever }
}
````

results in:

````
computed: {
  user () {
    return this.$store.state.user
  },
  age () {
    return this.$store.state.age
  },
  myOwnComputedProp() {  return whatever }
}
````
