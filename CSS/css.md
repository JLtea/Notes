# CSS Notes

### Units of Measurement

Absolute Units
`px`: pixel
`in`: inches
`cm`: centimeters
`mm`: millimeters
`pt`: points (1/72 of an inch)
`pc`: picas (12 points)

Relative Units
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
