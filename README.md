# Hellotickets Vue FlatPickr Component

[![license](https://badgen.net/github/license/ankurk91/vue-flatpickr-component)](https://yarnpkg.com/en/package/vue-flatpickr-component)

Vue.js component for [Flatpickr](https://flatpickr.js.org/) date-time picker

## [Demo](https://ankurk91.github.io/vue-flatpickr-component/) or [JSFiddle](https://jsfiddle.net/ankurk91/63kzdwLx/)

## Features
* Reactive ``v-model`` value
    - You can change flatpickr value programmatically 
* Reactive [config](https://flatpickr.js.org/options/) options
    - You can change config options dynamically
    - Component will watch for any changes and redraw itself
    - You are suggested to modify config via [Vue.set](https://vuejs.org/v2/api/#Vue-set)
* Can emit all possible [events](https://flatpickr.js.org/events/)
* Compatible with [Bootstrap](http://getbootstrap.com/), [Bulma](http://bulma.io/) or any other CSS framework
* Supports [wrapped](https://flatpickr.js.org/examples/#flatpickr-external-elements) mode
    - Just set ``wrap:true`` in config and component will take care of all
* Works with validation libraries

## Installation
```bash
# yarn
yarn add @hellotickets/vue-flatpickr-component

# npm
npm install @hellotickets/vue-flatpickr-component
```

## Usage
#### Minimal example
```html
<template>
  <div>
    <flat-pickr v-model="date"></flat-pickr>
  </div>
</template>

<script>
  import DatePicker from '@hellotickets/vue-flatpickr-component';
  import '@hellotickets/flatpickr/dist/flatpickr.css';
  
  export default {    
    data () {
      return {
        date: null,       
      }
    },
    components: {
      DatePicker
    }
  }
</script>
```

#### Detailed example
This example is based on Bootstrap 4 [input group](https://getbootstrap.com/docs/4.3/components/input-group/)
```html
<template>
  <section>
    <div class="form-group">
      <label>Select a date</label>
      <div class="input-group">
        <DatePicker
            v-model="date"
            :config="config"                                                          
            class="form-control" 
            placeholder="Select date"               
            name="date"
        />
        <div class="input-group-btn">
          <button class="btn btn-default" type="button" title="Toggle" data-toggle>
            <i class="fa fa-calendar">
              <span aria-hidden="true" class="sr-only">Toggle</span>
            </i>
          </button>
          <button class="btn btn-default" type="button" title="Clear" data-clear>
            <i class="fa fa-times">
              <span aria-hidden="true" class="sr-only">Clear</span>
            </i>               
          </button>
        </div>
      </div>
    </div>
    <pre>Selected date is - {{date}}</pre>
  </section>
</template>

<script>
  // bootstrap is just for this example
  import 'bootstrap/dist/css/bootstrap.css';
  // import this component
  import DatePicker from '@hellotickets/vue-flatpickr-component';  
  import '@hellotickets/flatpickr/dist/flatpickr.css';
  // theme is optional
  // try more themes at - https://flatpickr.js.org/themes/
  import 'flatpickr/dist/themes/material_blue.css';
  // localization is optional
  import {Hindi} from '@hellotickets/flatpickr/dist/l10n/hi.js';
  
  export default {
    name: 'yourComponent',
    data () {
      return {
        // Initial value
        date: new Date(),
        // Get more form https://flatpickr.js.org/options/
        config: {
          wrap: true, // set wrap to true only when using 'input-group'
          altFormat: 'M j, Y',
          altInput: true,
          dateFormat: 'Y-m-d',
          locale: Hindi, // locale for this instance only          
        },                
      }
    },
    components: {
      DatePicker
    },    
  }
</script>
```

#### As plugin
```js
  import Vue from 'vue';
  import VueFlatPickr from '@hellotickets/vue-flatpickr-component';
  import '@hellotickets/flatpickr/dist/flatpickr.css';
  Vue.use(VueFlatPickr);
```
This will register a global component `<flat-pickr>`

## Events
* The component can emit all possible events, you can listen to them in your component
```html
<DatePicker v-model="date" @on-change="doSomethingOnChange" @on-close="doSomethingOnClose" />
```
* Events names has been converted to kebab-case.
* You can still pass your methods in `:config` like original flatpickr do.

## Available props
The component accepts these props:

| Attribute        | Type                                            | Default              | Description      |
| :---             | :---:                                           | :---:                | :---             |
| v-model / value  | String / Date Object / Array / Timestamp / null | `null`               | Set or Get date-picker value (required) |
| config           | Object                                          | `{ wrap:false }`       | Flatpickr configuration [options](https://flatpickr.js.org/options/)|
| events           | Array                                           | Array of useful events  | Customise the [events](https://flatpickr.js.org/events/) to be emitted|

## Run examples on your localhost
* Clone this repo
* You should have node-js `10.13.0>=` and yarn `>=1.x` pre-installed
* Install dependencies `yarn install`
* Run webpack dev server `yarn start`
* This should open the demo page at `http://localhost:9000` in your default web browser

## Testing
* This package is using [Jest](https://github.com/facebook/jest) and [vue-test-utils](https://github.com/vuejs/vue-test-utils) for testing.
* Tests can be found in `__test__` folder.
* Execute tests with this command `yarn test`

## Changelog
Please see [CHANGELOG](CHANGELOG.md) for more information what has changed recently.

## Caveats
* :warning: Don't pass config option as inline literal object to `:config` prop.
```html
<!-- This will cause date picker to freeze -->
<DatePicker v-model="card" :config="{ dateFormat: 'd-m-Y H:i' }" />
```
* Vue.js can not detect changes when literal object/arrays passed within template, [see](https://github.com/vuejs/vue/issues/4060)

## License
[MIT](LICENSE.txt) License
