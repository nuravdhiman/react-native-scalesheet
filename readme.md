<p align="center">
	<img src="https://user-images.githubusercontent.com/23084841/27203532-ee8b7abc-51eb-11e7-95d3-5e76f276007d.png" />
</div>

# react-native-scalesheet

react-native-scalesheet is a utility module designed to be a drop-in replacement for `ScaleSheet.create` which aids in scaling components to maintain the same design across devices with varying resolutions. There are a few added features which you can make use of which you can read about in [Advanced Usage](#advanced-usage).

## Questions & Bug Reporting
If you happen to find any bugs or you have any questions, please feel free to create an [issue](https://github.com/ChristianTucker/react-native-scalesheet/issues) and I will get back to you as soon as possible. Please make sure to use the search function first to see if anyone else has reported the issue or asked the same question in the past. I will mark all questions with the `question` tag, so you can search efficiently. There is also a list of [common questions](#common-questions).

## <a name="installation-instructions">Installation Instructions</a>
```$ npm install --save react-native-scalesheet```

## <a name="example-usage">Example usage</a>
In order to use react-native-scalesheet you must import it in the JavaScript file that you wish to use it, to import react-native-scalesheet you simple do the following:
```javascript
import ScaleSheet from 'react-native-scalesheet';
```

To create a ScaleSheet you use the `ScaleSheet.create` function, which looks like this:

```javascript
import ScaleSheet from 'react-native-scalesheet';

const styles = ScaleSheet.create({
    container: {
        flex: 1,
        backgroundColor: 'black'
    }
});
```

How this would look in a React Component:

```javascript
import React from 'react';
import { View, Text } from 'react-native';

export default class ScalesheetExample extends React.Component {
    render() {
        return (
            <View style={styles.container}>
                <Text style={styles.label}>Hello ScaleSheet!</Text>
            </View>
        );
    }
}

const styles = ScaleSheet.create({
    container: {
        flex: 1,
        alignItems: 'center',
        justifyContent: 'center'
    },
    label: {
        fontWeight: '600',
        fontSize: 18,
        color: 'blue'
    }
});
```

## <a name="advanced-usage">Advanced Usage</a>
There are a few features that are added to the ScaleSheet object that helps with some styling, that is the addition of screen width/height injection as well as the option to pass an object instead of a normal style in order to ignore the scaling process.

### <a name="viewport-values">Viewport values</a>
Numeric values can be replaced with a string representation of the percentage of the screen's width or height that you would like to use, this can be done by adding `+ 'vh'` for the height of the screen and `+ 'vw'` for the width of the screen. The width and height variables are interchangeable, some examples can be found below.

```javascript
const styles = ScaleSheet.create({
    container: {
        // 82.5% of the devices width, can also be written as '82.5vw'
        width: 82.5 + 'vw',

        // 57% of the devices height, can also be written as 57vh
        height: 57 + 'vh',  

        // 20% of the devices height
        marginRight: '20vh'    
    }
});
```

Example of creating a square that is `50%` of the screens size in width and height:

```javascript
const styles = ScaleSheet.create({
    square: {
        width: '50vw',
        height: '50vw'
    }
});
```

### <a name="">Ignoring scaling on certain keys</a>
If for some reason you want to ignore the scaling on a certain object, let's say for example you want the `marginLeft` property to be exactly 20 units on all devices regardless of their resolution, you can pass the style as an object using the `{ ignored: true, value: ... }` syntax. Below is an example of a item that has the width and height scaled, but the marginLeft property is completely left alone.

**NOTE**: [Viewport values](#viewport-values) will not work while ignoring scaling and will result in a RedBox in development or crashes in production.

```javascript
const styles = ScaleSheet.create({
    example: {
        backgroundColor: 'red',
        width: 300,
        height: 300,
        marginLeft: { ignored: true, value: 25 }
    }
});
```

Please note that you should **NOT** pass an object as a value if you're going to set `{ ignored: false, ... }` while I could just as easily implement this to work, it's completely redundant and unnecessary, considering it's not ignored by default.

# <a name="common-questions">Common Questions</a>

 - Does this support nested styles and arrays, such as `transform`?
	 - Yes, this properly goes through your style object and recursively styles all items, using the lesser common style values such as `transform` and `shadowOffset` work just fine.
