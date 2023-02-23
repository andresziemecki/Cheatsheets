# Stateful Widgets

Change state over time.

The data that can change over time it's going to be store as state objects.

Shortcut to create one: `stful`

You will see that the `createState()` function instantiate a State object.

Inside the state widget we can define data and change it over time.

To change the state, whenever an event happend which call a function, possibly we'll need to add a `setState(){}` inside of that event.

# Widget LifeCycle

## Stateless

- Doesnt run states over time
- build only runs once

## Stateful

- Run states over time
- Where the setState() triggers the build function

### initState

Only call once when the widget is created.

We can use it to suscribe to streamings or object that could change our data

### build

Builds the widget tree

A build is triggered every time we use setState


## Dispose

Executed when the widget or the object is completely removed

# Running all method will execute the following:

1. initState
2. build
3. When executing setState we are going to see the build again executed