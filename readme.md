[![npm](https://img.shields.io/npm/dt/vue-owl-carousel.svg)](https://www.npmjs.com/package/vue-owl-carousel)

---

## Intro

- The [VueJS](https://vuejs.org/) wrapper for [Owl Carousel](https://owlcarousel2.github.io/OwlCarousel2/).

* [Owl Carousel](https://owlcarousel2.github.io/OwlCarousel2/) is touch enabled jQuery plugin that lets you create a beautiful responsive carousel slider.

* Extended from [vue-owl-carousel](https://github.com/s950329/vue-owl-carousel)

## what has changed in this fork?

- Added `rtl` prop, can be changed dynamically (the carousel will be re-instantiated in rtl mode and on the same slide location)

- Due to a bug in the responsive mode, i've added a temporarily fix by allowing `items` prop to be changed dynamically (like `rtl`), so you can determine the breakpoints and pass corresponding items from your main project.

- Fixed `initialize` & `initialized` not being fired up.

- Added a `events` prop that takes an array of the events you want to register instead of registering all library events.

```
<carousel :events="['initialized', 'changed']" @initialized="intial" @changed="changed">
//
</carousel>

<script>
import carousel from 'xx-vue-owl-carousel'
export default {
    components: { carousel },
    methods:{
        intial(event) {
        console.log('owl carousel initialized')
        console.log('number of slides:', event.item.count)
        console.log('active slide index:', event.item.index)
        },
        changed(event){
        //
        }
    }
}
</script>
```

- changed `webpack` to `rollup`.

## Installation

`npm i -s xx-vue-owl-carousel` or `yarn add xx-vue-owl-carousel`

## Usage

```
<script>

import carousel from 'xx-vue-owl-carousel'

export default {
    components: { carousel },
}

</script>
```

Basic Usage

```
<carousel>

    <img src="https://placeimg.com/200/200/any?1">

    <img src="https://placeimg.com/200/200/any?2">

    <img src="https://placeimg.com/200/200/any?3">

    <img src="https://placeimg.com/200/200/any?4">

</carousel>
```

Custom prev and next buttons using slot, the buttons will be hidden while start and end in non-loop mode

```
<carousel>

    <template slot="prev"><span class="prev">prev</span></template>

    //

    <template slot="next"><span class="next">next</span></template>

</carousel>
```

Set options,

```
<carousel :autoplay="true" :nav="false">

//

</carousel>
```

Set events,

```
<carousel @changed="changed" @updated="updated">

//

</carousel>
```

## Available options

Currently following options are available.

- ### items

type : `number`

default : `3`

The number of items you want to see on the screen.

- ### margin

type : `number`

default : `0`

Margin-right (px) on item.

- ### loop

type : `boolean`

default : `false`

Infinity loop. Duplicate last and first items to get loop illusion.

- #### center

Type: `Boolean`

Default: `false`

Center item. Works well with even an odd number of items.

- #### nav

Type: `Boolean`

Default: `false`

Show next/prev buttons.

- #### autoplay

Type: `Boolean`

Default: `false`

Autoplay.

- #### autoplaySpeed

Type: `Number/Boolean`

Default: `false`

Autoplay speed.

- #### rewind

Type: `Boolean`

Default: `true`

Go backwards when the boundary has reached.

- #### mouseDrag

Type: `Boolean`

Default: `true`

Mouse drag enabled.

- #### touchDrag

Type: `Boolean`

Default: `true`

Touch drag enabled.

- #### pullDrag

Type: `Boolean`

Default: `true`

Stage pull to edge.

- #### freeDrag

Type: `Boolean`

Default: `false`

Item pull to edge.

- #### stagePadding

Type: `Number`

Default: `0`

Padding left and right on stage (can see neighbours).

- #### autoWidth

Type: `Boolean`

Default: `false`

Set non grid content. Try using width style on divs.

- #### autoHeight

Type: `Boolean`

Default: `false`

Set non grid content. Try using height style on divs.

- #### dots

Type: `Boolean`

Default: `true`

Show dots navigation.

- #### autoplayTimeout

Type: `Number`

Default: `5000`

Autoplay interval timeout.

- #### autoplayHoverPause

Type: `Boolean`

Default: `false`

Pause on mouse hover.

- #### responsive

Type: `Object`

Default: `{}`

Example : `:responsive="{0:{items:1,nav:false},600:{items:3,nav:true}}"`

Object containing responsive options. Can be set to false to remove responsive capabilities.
