# ResponsiveImage
A responsive Image component that chooses the best-resolution image for the current screen.

## Installation

```
yarn add @exponent/react-native-responsive-image
```

Import it with:

```js
import ResponsiveImage from '@exponent/react-native-responsive-image';
```

## Usage

ResponsiveImage accepts the same props as Image plus a new prop called `sources`. The `sources` prop is an object whose keys are pixel ratios (that is, screen scales like "2" or "3"). Its values are Image sources to display on screens with the respective pixel ratio. This is how you use it:

```js
<ResponsiveImage
  sources={{
    // The values are anything that Image's source prop accepts
    2: require('image!icon@2x.png'),
    3: { uri: 'https://example.com/icon@3x.png' },
  }}
  // (optional) force ResponsiveImage to load a specified pixel ratio
  preferredPixelRatio={2}
  // (optional) specify a custom function for rendering the image. You control
  // the props that are passed to the custom component. By default, React
  // Native's Image component is rendered.
  renderImageElement={(props) => <CustomImage {...props} />}
/>
```

## Implementation

ResponsiveImage chooses the image source for the closest pixel ratio that is greater than or equal to screen's pixel ratio. You will get a crisp image while conserving bandwidth and system resources.

As an example, if you were to provide 2x and 3x sources as in the Usage example, these are the pixel ratios that ResponsiveImage will choose for various screens:

Screen Scale  | Chosen Pixel Ratio
------------- | --------------------------
1x            | 2x (use lowest available)
2x            | 2x (exact match)
2.5x          | 3x (round up to nearest)
3x            | 3x (exact match)
4x            | 3x (use highest available)
