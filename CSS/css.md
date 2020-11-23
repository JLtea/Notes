# CSS Notes

### Units of Measurement

**Absolute Units**

`px`: pixel

`in`: inches

`cm`: centimeters

`mm`: millimeters

`pt`: points (1/72 of an inch)

`pc`: picas (12 points)

**Relative Units**

`%`: percentage of parent element

`vw`: viewport width

`vh`: viewport height

`rem`: root (<html>) element

`em`: the width of a capital letter M of the font-size of the parent element

`ch`: width of the character zero (“0”)

`ex`: the current x-height of the current font or the half of 1em

### Media Queries

Use @media queries for responsive layout

```
@media (min-width: 600px) {
  .cardLayout {
    grid-template-columns: repeat(2, 47%);
  }
}
@media (min-width: 900px) {
  .cardLayout {
    grid-template-columns: repeat(3, 30%);
  }
}

/* can use screen resolution of the device itself (dots per inch)*/
@media only screen and (min-resolution: 192dpi) {
  /* Style stuff */
}
```

### Other

clamp (min, curr, max)

```
font-size : clamp(1rem, 40px, 4rem)
```

## Animations

@keyframes Properties:

- `animation-duration` how long animation should take
- `animation-delay` delay before start of animation (negative values will start in middle of animation)
- `animation-iteration-count` number of times animation should run (`infinite` will loop animation)
- `animation-direction` whether animation should be played `normal` | `reverse` | `alternate` | `alternate-reverse`
- `animation-timing-function` specifies the speed curve (`ease` default)
- `animation-fill-mode` specifies style when animation is not playing
- `from` (same as `0%`)
- `to` (same as `100%`)

Example

```
/*animation code*/
@keyframes example {
  from {background-color: red;}
  to {background-color: yellow;}
}

div {
  width: 100px;
  height: 100px;
  background-color: red;
  animation-name: example; // bind animation to element
  animation-duration: 4s;
}
```
