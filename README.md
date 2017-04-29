react-sticky [![Build Status](https://travis-ci.org/captivationsoftware/react-sticky.svg?branch=master)](https://travis-ci.org/captivationsoftware/react-sticky)
============

Make your React components sticky!

#### Demos
  - [Basic](http://rawgit.com/captivationsoftware/react-sticky/6.0.0/examples/basic/index.html)
  - [Relative](http://rawgit.com/captivationsoftware/react-sticky/6.0.0/examples/relative/index.html)
  - [Stacked](http://rawgit.com/captivationsoftware/react-sticky/6.0.0/examples/stacked/index.html)

#### Version Highlights
  - 6.x has been overhauled to support sticky behavior via higher-order component, giving you ultimate control of implementation details
  - Features a minimal yet efficient API
  - Drops support for versions of React < 15.3. If you are using an earlier version of React, continue to use the 5.x series

## Installation
```sh
npm install react-sticky
```

## Overview & Basic Example
`<Sticky />` elements should contain a function as its immediate child, which itself returns an element.
This function will be called based on events of the parent `<StickyContainer />`, and will provide
sane defaults for basic sticky functionality, along with a hook to apply your own logic / customizations.  

app.js
```js
import React from 'react';
import { StickyContainer, Sticky } from 'react-sticky';
...

class App extends React.Component ({
  render() {
    return (
      ...
      <StickyContainer>
        ...
        <Sticky>
          {
            ({ isSticky, wasSticky, style, distanceFromTop, distanceFromBottom, calculatedHeight }) => {
              return (
                <header style={style}>
                  ...
                </header>
              )
            }
          }
        </Sticky>
        ...
      </StickyContainer>
      ...
    );
  },
});

```

When the "stickiness" becomes activated, the arguments to the sticky function
are modified. Similarly, when deactivated, the arguments are once again restored accordingly.

### `<StickyContainer />` Props
`<StickyContainer />` supports all valid `<div />` props.  

### `<Sticky />` Props

#### relative _(default: false)_
Set `relative` to `true` if the `<Sticky />` element will be rendered within
an overflowing `<StickyContainer />` (e.g. `style={{ overflowY: 'auto' }}`) and you want
the `<Sticky />` behavior to react to events only within that container.

#### topOffset _(default: 0)_
Sticky state will be triggered when the top of the element is `topOffset` pixels from the top of the closest `<StickyContainer />`. Positive numbers give the impression of a lazy sticky state, whereas negative numbers are more eager in their attachment.

app.js
```js
<StickyContainer>
  ...
  <Sticky topOffset={80}>
    { ({ isSticky, wasSticky, style, distanceFromTop, distanceFromBottom, calculatedHeight }) => (...) }
  </Sticky>
  ...
</StickyContainer>
```

The above would result in an element that becomes sticky once its top is greater than or equal to 80px away from the top of the `<StickyContainer />`.

#### bottomOffset _(default: 0)_
Sticky state will be triggered when the bottom of the element is `bottomOffset` pixels from the bottom of the closest `<StickyContainer />`.

app.js
```js
<StickyContainer>
  ...
  <Sticky bottomOffset={80}>
    { ({ isSticky, wasSticky, style, distanceFromTop, distanceFromBottom, calculatedHeight }) => (...) }
  </Sticky>
  ...
</StickyContainer>
```

The above would result in an element that ceases to be sticky once its bottom is 80px away from the bottom of the `<StickyContainer />`.

#### disableCompensation _(default: false)_
Set `disableCompensation` to `true` if you do not want your `<Sticky />` to correct any
jumpy behavior as its attachment changes across sticky state changes.

app.js
```js
<StickyContainer>
  ...
  <Sticky disableCompensation>
    { ({ isSticky, wasSticky, style, distanceFromTop, distanceFromBottom, calculatedHeight }) => (...) }
  </Sticky>
  ...
</StickyContainer>
```


#### disableHardwareAcceleration _(default: false)_
When `disableHardwareAcceleration` is set to `true`, the `<Sticky />` element will not use hardware acceleration (e.g. `transform: translateZ(0)`). This setting is not recommended, and can usually be
avoided by improving the structure of your DOM.

app.js
```js
<StickyContainer>
  ...
  <Sticky disableHardwareAcceleration>
    { ({ isSticky, wasSticky, style, distanceFromTop, distanceFromBottom, calculatedHeight }) => (...) }
  </Sticky>
  ...
</StickyContainer>
```

### License
MIT
