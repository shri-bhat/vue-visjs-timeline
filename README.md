# Vue-visjs-timeline
Vue component for the [vis.js](http://visjs.org/) timeline module.

### Installation
```
npm i -- save vue-visjs-timeline
```

### Basic usage
Import and declare the component
```javascript
import timeline from 'vue-visjs-timeline'
Vue.component('timeline', timeline)
```
Add the component in the template.
```html
<template>
    <timeline v-bind:items="items" v-bind:groups="groups"></timeline>
</template>
```
Create items and groups data in the component.
```javascript
export default {
	name: 'home-page',
	data() {
		return {
			groups: [
			    {id: 'a1', content:'Group one'},
			    {id: 'a2', content:'Group two'},
			    {id: 'a3', content:'Group three'}
			],
			items: [
			    {id: 'a1', content: 'Item one', group: 'Group one'},
			    {id: 'a2', content: 'Item two', group: 'Group two'},
			    {id: 'a3', content: 'Item three', group: 'Group three'}
			]
		}
	}
}
```

#### Styling
Custom CSS added to enhance the UI. Import custom CSS
```
require('../node_modules/vue-visjs-timeline/dist/vue-visjs-timeline.css')
```

#### Configure tools
Tools is group of options (Go today, Zoom in, Zoom out). Enabled by default. Add the configuration to disable.
```
<timeline v-bind:items="items" v-bind:groups="groups" :hide-tools=true></timeline>
```
#### Events
This event is triggered when item is moved or changed
```
<timeline v-bind:items="items" v-bind:groups="groups" v-on:item-move="updateItem"></timeline>

export default {
	name: 'home-page',
	methods: {
	    updateItem: function (item) {
	        // handle the event
	    }
	}
}
```

#### Supported events
Note: Only limited events are supported for now

| Events        | Description               |
| --- |---|
| v-on:item-move | On item position change |
| v-on:range-changed | On window zoom in/out or move|

#### Supported props
Note: Only limited props are enabled

| Name        | Description |
| --- |---|
| v-bind:items | List of items |
| v-bind:groups | List of groups |
| v-bind:option | Timeline option (If not present default option is added) |
| v-bind:start | Window start (Timestamp/moment date) |
| v-bind:end | Window end (Timestamp/moment date) |
| :hideTools | Force tools to hide |
