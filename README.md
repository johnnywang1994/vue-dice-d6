# vue-dice-d6

A d6 vue dice component with animation setted for easily usage

the component used `scss` for developing, remember to install the node-sass.


## Install

``` bash
npm install vue-dice-d6
// or
yarn add vue-dice-d6
```

import component

```js
import DiceD6 from 'vue-dice-d6';

export default {
  components: {
    DiceD6
  }
};
```


## Usage

Give the dice width, height

```html
<template>
  <div id="app">
    <button @click="toggleResult">Toggle Dice</button>
    <dice-d6 size="s" :result="result" :start="start" />
  </div>
</template>

<script>
import DiceD6 from 'vue-dice-d6';

export default {
  components: {
    DiceD6,
  },
  data () {
    return {
      result: 1,
      start: false,
    };
  },
  methods: {
    toggleResult() {
      // if dice is animating
      if (this.start) {
        // use setTimeout for stopped transition
        setTimeout(() => {
          this.result = Math.ceil(Math.random() * 6);
        });
      }
      this.start = !this.start;
    },
  },
};
</script>

<style>
.dice-wrapper {
  width: 100px;
  height: 100px;
}
</style>
```


## Props

### result

Result Dice Point

  - type: `Number`
  - default: 1


### start

whether Start Dice Animation

  - type: `Boolean`
  - default: false


### diceBg

Dice background image url

give an image as the dice's background, will used for all 6 sides.

  - type: `String`


### dicePoint

Dice point image url

give an image as the dice's dots background, dots will auto positioned.

  - type: `String`


### size

Dice size options

  - type: `String`
  - default: `s`
  - allowed values: `xs`, `s`, `m`, `l`, `xl`


### scrollType

Dice animation type

  - type: `String`
  - default: `random`
  - allowed values: `random`, `round`


## License

[MIT](http://opensource.org/licenses/MIT)

Copyright (c) 2020-present, Johnny Wang
