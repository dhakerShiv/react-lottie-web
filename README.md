# Lottie Animation View for React

[![npm version](https://badge.fury.io/js/react-web-lottie.svg)](http://badge.fury.io/js/react-web-lottie)

## What's new
Added ```lottiRef``` as new param to fully control lottie animation, you can use any [lottie-web](https://github.com/airbnb/lottie-web) methods on it.

## Wapper of bodymovin.js

[bodymovin](https://github.com/bodymovin/bodymovin) is [Adobe After Effects](http://www.adobe.com/products/aftereffects.html) plugin for exporting animations as JSON, also it provide bodymovin.js for render them as svg/canvas/html.

## Why Lottie?

#### Flexible After Effects features
We currently support solids, shape layers, masks, alpha mattes, trim paths, and dash patterns. And we’ll be adding new features on a regular basis.

#### Manipulate your animation any way you like
You can go forward, backward, and most importantly you can program your animation to respond to any interaction.

#### Small file sizes
Bundle vector animations within your app without having to worry about multiple dimensions or large file sizes. Alternatively, you can decouple animation files from your app’s code entirely by loading them from a JSON API.

[Learn more](http://airbnb.design/introducing-lottie/) › http://airbnb.design/lottie/

Looking for lottie files › https://www.lottiefiles.com/

## Installation

Install through npm:
```
npm install --save react-web-lottie
```

## Usage

Basic example

```jsx
import React, { useRef } from "react";
import LottieDemo from "react-web-lottie";
import animationData from "./animation.json";

export default function Animation() {
  const animationRef = useRef(null);

  const defaultOptions = {
    loop: false,
    autoplay: true,
    animationData: animationData,
    rendererSettings: {
      preserveAspectRatio: "xMidYMid slice"
    }
  };

  return (
    <LottieDemo
      lottiRef={animationRef}
      width={600}
      height={500}
      options={defaultOptions}
      isClickToPauseDisabled={true}
    />
  );
}
```

Update text dynamically

Note: you need to deselect glyphs option while exporting JSON from After effects to make it work.

App.js

```jsx
import React, { useState } from "react";
import Animation from "./Animation.js";

export default function App() {
  const [email, setEmail] = useState("");

  return (
    <React.Fragment>
      <div>
        Email
        <input
          type="text"
          height="100"
          onKeyUp={(event) => setEmail(event.target.value)}
        />
      </div>
      <Animation email={email} />
    </React.Fragment>
  );
}
```

Animation.js

```jsx
import React, { useRef, useEffect } from "react";
import LottieDemo from "react-web-lottie";
import animationData from "./animation.json";

export default function Animation({ email = "" }) {
  const animationRef = useRef(null);

  useEffect(() => {
    // Update according to you [startFrame, endFrame]
    animationRef.current.playSegments([89, 90], true);
    let element,
      elementIndex = 1, // Layer number from your json
      frameIndex = 0; // frame index in your layer, mostly it will be 0 only

    // Below part depends on how lotti animation has been created in after effects
    element = this.animationRef.current.renderer.elements[layerIndex];
    element.updateDocumentData({ t: email }, frameIndex);
  }, [email]);

  const defaultOptions = {
    loop: false,
    autoplay: true,
    animationData: animationData,
    // Change below one as you need, you can even remove it if you do not need
    initialSegment: [0, 90], // [startFrame, endFrame]
    rendererSettings: {
      preserveAspectRatio: "xMidYMid slice"
    }
  };

  return (
    <LottieDemo
      width={800}
      height={500}
      lottiRef={animationRef}
      options={defaultOptions}
      isClickToPauseDisabled={true}
    />
  );
}
```

### props
The `<Lottie />` Component supports the following components:

**options** *required*

the object representing the animation settings that will be instantiated by bodymovin. Currently a subset of the bodymovin options are supported:

>**loop** *options* [default: `false`]
>
>**autoplay** *options* [default: `false`]
>
>**animationData** *required*
>
>**rendererSettings** *required* 

**width** *optional* [default: `100%`]

pixel value for containers width.

**height** *optional* [default: `100%`]

pixel value for containers height.

**eventListeners** *optional* [default: `[]`]

This is an array of objects containing a `eventName` and `callback` function that will be registered as  eventlisteners on the animation object. refer to [bodymovin#events](https://github.com/bodymovin/bodymovin#events) where the mention using addEventListener, for a list of available custom events.

example:
```jsx
eventListeners=[
  {
    eventName: 'complete',
    callback: () => console.log('the animation completed:'),
  },
]
```

## Related Projects

* [Bodymovin](https://github.com/bodymovin/bodymovin) react-web-lottie is a wrapper of bodymovin

## Contribution
Your contributions and suggestions are heartily welcome.

## License
MIT

