# Elemental Grid System

The elemental grid system can be used to create a semantic grid system that fits your needs rather than trying to adapt
an existing solution.

## Building The Grid

Building the grid is simple, use the following command to generate the basic grid style as well as create the mobile
defaults for the grid.

```scss
@include grid-default(); // generate grid default styling.

@include generate-layout(); // generate grid styles
```

The Elemental Grid does not make any assumptions about how you want to display your content at different screen
resolutions. As a result you are responsible
for wrapping the grid layouts in media queries to achieve the desired results.

```scss
// only display grid if over 800px, otherwise elements will appear to be stacked.
@media (min-width: 800px) {
    @include generate-layout();
}
```

By default there are 1,2 and 12 column layouts generated. These can be accesed easily with the following html.

```html
<div class="row">
    <div class="col-1"></div>
</div>
<div class="row">
    <div class="col-1-2"></div>
    <div class="col-1-2"></div>
</div>
<div class="row">
    <div class="col-3-13"></div>
    <div class="col-6-12"></div>
    <div class="col-3-12"></div>
</div>
```
Other grid layouts it can be be easily acessed by simply using the proper fractional value. Ex.
`col-2-12`, `col-3-4`, etc...

If you wish to add padding to a particular row you can apply the class of `pad` to the row element.

```html
<div class="row pad">
    <div class="col-3-13"></div>
    <div class="col-6-12"></div>
    <div class="col-3-12"></div>
</div>
```

### Right to Left

Right to left functionality is supported by default by adding the class `.rtl` to the row element.

```html
<div class="row rtl pad">
    <div class="col-2-13"></div>
    <div class="col-3-12"></div>
    <div class="col-7-12"></div>
</div>
```


## Customizing the Grid

You have full control over how the grid rendered at different breakpoints, as well how the grid itself is built. You can
generate any layout you wish, and as many as you wish.

```scss
$layouts: 8,10;
@include generate-layout($layouts); // This would generate an 1, 2, 8 and 10 column layout with the default `col` prefix

@include generate-layout($layouts, 'med'); // Generates a 1, 2, 8, and 10 column layout with a prefix of `med`.
```

Similarly you can add a prefix to the layout classes if you wish to denote different layouts for each breakpoint.

```scss
$small-layouts: 3;
$medium-layouts: 3,4;
$large-layouts: 3,4,12;

@media (max-width: 479px) {
    // mobile
    @include generate-layout($small-layouts, 'small');
}
@media (min-width: 480px) and (max-width: 799px) {
    // small tablet
    // generates 1, 2, 3, 4, and 8 column layouts accessible with the medium-x-y prefix
    @include generate-layout($medium-layouts, 'medium'); // generates 1, 2, 3, 4, and 8 column layouts
}
@media (min-width: 800px) {
    // desktop
    // generates 1, 3, 4, and 12 column layouts accessible with the col-x-y prefix
    @include generate-layout($large-layouts);
}
scss

Accompanying HTML

```html
<div class="row">
    <div class="col-1-4 medium-3-4 small-col-2-3"></div>
    <div class="col-1-4 medium-1-4 small-col-1-3"></div>
    <div class="col-1-4 medium-3-4"></div>
    <div class="col-1-4 medium-3-4"></div>
</div>
```

## Default Values
Default values for the grid are below but can be overridden in your stylesheets.

```scss
$elemental-grid-padding: 10px; // defines the padding for the row element when .pad is applied
$elemental-grid-gutter: 10px; // defines the defalt gutter for the grid
$elemental-grid-column-margin-top: 0px;
$elemental-grid-column-margin-bottom: 5px;
$elemental-grid-default-column-name: 'col'; // default css class prefix
$elemental-grid-layouts: 3,4,12; // default grid column layouts that are generated
```

## Utility Classes

`.(prefix)-first`: Generated with each layout to remove the gutter for the first element in a particular row. This is
useful if a particular column is the first in row at a lower resolution. The default is `.col-first` but if you choose a
custom prefix it will be available with that prefix. Ex. `.medium-first`, `.small-first`.

```html
<div class="row pad">
    <div class="col-1-12"><div class="content"></div></div>
    <div class="col-2-12 medium-2-4 small-2-3"><div class="content"></div></div>
    <div class="col-3-12 medium-2-4 small-1-3"><div class="content"></div></div>
    <!-- .small-first and .medium-first removes the left gutter when the colum is pushed to the next row -->
    <div class="col-3-12 medium-3-4 small-1-3 medium-first small-first"><div class="content"></div></div>
    <div class="col-2-12 medium-1-4 small-2-3"><div class="content"></div></div>
    <div class="col-1-12"><div class="content"></div></div>
</div>
```