# Picasa album notes

## current (1/5/15) blockage

the `<picture>` element, created by the [picturefill js library](https://github.com/scottjehl/picturefill), when used inside a web component does not get the container width and thus chooses the smallest image in the list

### public queries:
* http://stackoverflow.com/questions/27785795/picturefill-element-inside-a-polymer-web-component-loses-container-dimensions
* https://github.com/scottjehl/picturefill/issues/412

### example code:
http://codepen.io/scottnath/pen/RNoBXd