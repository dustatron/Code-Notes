# Sass Notes

[setup video](https://www.youtube.com/watch?v=2QaI5ajg4Hw)

## Sass Tools

### Basic Reset

```scss
/* Basic Reset */
*,
*::after,
*::before {
    margin: 0;
    padding: 0;  
    box-sizing: inherit;
}
```

### Set font size to make 1rem = 10px

This will require the [responsive mixin](#Responsive) 

```scss
html {
    // this defines what 1rem is
    font-size: 62.5%; // 1rem = 10 px

    @include respond(tab-land) {
        font-size: 56.25%; // 1rem = 9px, 9/16 =
    }

    @include respond(tab-port) {
        font-size: 50%; // 1rem = 9px, 9/16 =
    }

    @include respond(big-desktop) {
        font-size: 75%; // 1rem = 12px, 12/16 = 75
    }
}
```



## Variables

start with $

```css
$red-color: red
```

## Mixin 

```scss
@mixin flexCenter($direction, $background) {
  display: flex;
  flex-direction: $direction;
  background: $background
}

header {
  @include flexCenter(column, blue);
}
```

### *mixin tools*

#### Clearfix

```scss
@mixin clearfix {
    &:after{
        content: "";
        display: table;
        clear: both;
    }
}


```

#### Absolute Center

```scss
@mixin absCenter {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}
```



#### Responsive

```scss
// Media Query Manager
/*

0-600 = phone
900-1200 = tablet
1200-1800 = desktop
1800 + big desktop

$breakpoint argument choices:
 - phone
 - tab-port
 - tab-land
 - big-desktop

 ORDER: base + typography > gerneral layout + grid > page layout > components

*/
@mixin respond($breakpoint) {
    @if $breakpoint == phone {
        @media (max-width: 37.5em) { @content; } //600px
    } 
    @if $breakpoint == tab-port {
        @media (max-width: 56.25em) { @content; } //900px
    } 
    @if $breakpoint == tab-land {
        @media (max-width: 75em) { @content; } //1200
    } 
    @if $breakpoint == big-desktop {
        @media (min-width: 112.5em) { @content; }  //1800
    } 
}
```





## Inherit 

this will allow an item to receive all properties from another item.
You are allowed to overwrite any item you would like.

```scss
@import './header';

.contact {
	@extend header;
}
```

