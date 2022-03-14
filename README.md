# react-hook-absolute-orientation

A React hook to access data from the [Absolute Orientation Sensor API](https://developer.mozilla.org/en-US/docs/Web/API/AbsoluteOrientationSensor).

## Installation

Using `npm`:

```sh
npm install --save react-hook-absolute-orientation
```

Using `yarn`:

```sh
yarn add react-hook-absolute-orientation
```

## Usage

```jsx
import React from 'react'
import useAbsoluteOrientationSensor from 'react-hook-absolute-orientation'

const onUpdate = info => {
  console.log('NEW INFO: ', info)
}

const ComponentWithGyroscope = () => {
  const quaternion = useAbsoluteOrientationSensor(
    { frequency: 3, referenceFrame: 'device' },
    onUpdate // named function reference is required
  )

  return (
    <div>
      <div>Absolute Orientation Sensor Hook Demo</div>
      <pre>{JSON.stringify(quaternion, null, 2)}</pre>
      <div>
        Rounded to 0.01
        {quaternion.map((item, index) => {
          return <div key={index}>{Math.round(100 * item) / 100}</div>
        })}
      </div>
      <div>
        Rounded to 0.1
        {quaternion.map((item, index) => {
          return <div key={index}>{Math.round(10 * item) / 10}</div>
        })}
      </div>
    </div>
  )
}
```

### Using `SensorOptions`

https://w3c.github.io/orientation-sensor/#absoluteorientationsensor-interface

If you want to use this feature, simply provide `useGyroscope` with a `SensorOptions` object:

```jsx
const sensor = useAbsoluteOrientationSensor({
  frequency: 10, // cycles per second
  referenceFrame: 'device', // or 'screen'
})
```

### Using a callback function

You can supply a second parameter to `useGyroscope` which will be called every time the data from the Gyroscope API is updated. This callback function is then called with the `gyroscope` object with all its properties.

If you don't use `SensorOptions`, supply `{}` as your first argument.

```jsx
const onUpdate = data => {
  console.log('Here’s some new data from the API: ', data)
}

const sensor = useAbsoluteOrientationSensor({}, onUpdate)
```

## Caveats

Absolute Orientation Sensor API is available only in secure contexts (a.k.a. only using HTTPS).

## Credits

Credit to [Bence A. Tóth](https://github.com/bence-toth) for his original hook code for [Geolocation](https://www.npmjs.com/package/react-hook-geolocation).

## License

LGPL-3.0
