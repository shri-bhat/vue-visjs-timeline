<template>
  <div id="timeline" style="height:100%">
    <div class="tools vs-btn-group" v-if="hideTools!=true">
			<button type="button" class="vs-btn vs-btn-light" @click="goToday()"><img width="15" src="data:image/png;base64,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"></button>
			<button type="button" class="vs-btn vs-btn-light" @click="zoomIn()"><img width="15" src="data:image/png;base64,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"></button>
			<button type="button" class="vs-btn vs-btn-light" @click="zoomOut()"><img width="15" src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAF0AAABdCAYAAADHcWrDAAAE0UlEQVR4nO2cvY5cRRCFT49WKzSRIyJLlhwjIgfkkPEKjvcGfgLjmBcguxOQEZAiAr8DiROIkGVZjizLsggI0GqbYOZKRU2d6l7bUAHnk1Y7t2//VJ/uPl3etd06OsR/y646gP8jEr0AiV6ARC9Aohcg0QuQ6AVI9AIkegESvQCJXoBEL0CiFyDRC5DoBUj0AiR6ARK9AIlegEQvQKIXINELkOgFSPQCJHoBEr0AiV6ARC9Aohcg0QuQ6AVI9AIkegESvYCL7OVytVwAeADg6977fQD71hp672it/aNuVJaV+/dZvVGdmT7+ZW4AvAbwC4Cf18P6Oqvc2L85Wq6Wi977N621BcAdAJ8A2PV+rD8j8KxY9jkM0vTBxojGZP3M4OuyOE35X733PwH81lp7tB7WZ7TvSPTlarkE8OQk+oWfHPs8YiSQ7TOabNRu9nREMWfvWNyTG+glgC/Xw/p7FBvz9AcAHsLYjx0oCmpmB40Wx4tvF8R+t+/9u+gk2tiiBY0Ww35Fsfm5u1jv9t4fn+z5DObpXwH4dEakD93l0UQsvk5Ud+Yde7axzMQzGeMOwBcA7gJ44euznX4PwD7awdFO8bvBf7Z1t3d2R21l9ov1zepHMfh67NnHlsVly7wGrs4eR9HPYKJfsneZ72YWZCcVHdGoH38aotMRffexZf1F8/PzYGU+djfODsfk44xhns7Em/XnrJ2fTOSfbKf799u7zJe3OtEmYaclOhH+RGaLHEHzdDZJHwBjxhdHWYotz96zS47596j/URY1GsffER660+2xio4XI1pddi+MdnrUhvkqyzLY7s2eZ+Nn8Y423Ef/McBMru2PqS+PbCPKy1k9++xjiWJkNpPNcbQQGemPAdilx/6QYcsir2Nt2MT856yPmXQxu0gjmxp5czS3GcKdnu2AbCK+TWRNtn8WZHSRve9zFKefC3vO4mKezbIiS5oWsvKRJ/vPvo0fI8saZvuLfJp9ZmJnzN4JM/0NPT3a9aM8e/s8k53c5l2UFWQezBYiWrAZ4W1b2/8o8/GEnj4rlg94FEB2odp74H36y2xuhB13JhEYjTdaRGovVoRs1UYTjQK4zSlgu5L1mVkUiy2zMmYjUeYUtLuJxmX28geAazshH8TIPyMPz7xwe565iCwsQ/LPUYwjwX2cfiMyKzmVX+Oo4xkse/m19x42GN3YLCXbynzdqO02EXZJj+Kx9aOTEcXArM+3yRbMxfkGwU8YAW4vT1trz/1gkdXMWI9vOzNBloePToK3xpnY7Fy8r9tnv0BR+Wnc69baj+thfRONzezlRe/9Se/9XTSYH3AkxuiOsLsyWhy/6FH24ttmx5/ZHNvNUd/s+dTPTwC+J9qmvyPd4fgbpG8BfAbgsve+y1KiyA6ybMBOlNlRJN4oy/Flt7kjvPVE4xCLuW6tvQXwA4Dv1sP6jo4x+s8wl6tlD+BzAPcB7KNJkovkLNDbpHGW2T4+ZIzZGEj5DY4e/gzAq/WwhlnLxlB08fHRXzYqQKIXINELkOgFSPQCJHoBEr0AiV6ARC9Aohcg0QuQ6AVI9AIkegESvQCJXoBEL0CiFyDRC5DoBUj0AiR6ARK9AIlegEQvQKIXINELkOgFSPQCJHoBEr0AiV6ARC9AohfwN19oIqZEyyUyAAAAAElFTkSuQmCC"></button>
		</div>
  </div>
</template>

<style src="./style.css"></style>

<script>
import vis from 'vis'

export default {
  name: 'timeline',
  props: {
    items: {required: true},
    groups: {required: false},
    option: {required: false},
    start: {required: false},
    end: {required: false},
    hideTools:{required: false}
  },
  data: function () {
    return {
      timeline: null,
      timelineData: {
        items: [],
        groups: [],
        option: {
					onMove: item => { this.$emit('item-move', item)},
					editable: {
						add: false,
						updateTime: true,
						updateGroup: false,
						remove: false,
						overrideItems: false
					},
					orientation: 'top',
					height: '100%',
					verticalScroll: true,
					horizontalScroll: true,
					zoomKey: 'ctrlKey',
					zoomMax: 160000000000,
					zoomMin: 100000000,
					showTooltips: true
				}
      }
    }
  },
  watch: { 
    items: function(items) {
      this.timelineData.items = new vis.DataSet(items)
      this.updateTimeline()
    },
    groups: function(groups) {
      this.timelineData.groups = groups
      this.updateTimeline()
    }
  },
  methods: {
    goToday: function() {
      this.timeline.moveTo(this.$moment());
    },
    zoomIn: function () {
      this.timeline.zoomIn(0.4);
    },
    zoomOut: function () {
      this.timeline.zoomOut(0.4);
    },
    initTimeline: function () {
      var container = document.getElementById('timeline');
    
      // Create a Timeline
      if (!this.timeline) {
        this.timeline = new vis.Timeline(container, this.timelineData.items, this.timelineData.groups, this.timelineData.option);
        this.timeline.on('rangechanged', e => {this.$emit('range-changed', e)});
      }
    },
    updateTimeline: function () {
      if (this.timeline) {
        this.timeline.setData({groups: this.timelineData.groups, items: this.timelineData.items})
      }
    }
  },
  mounted: function() {
    // If not present use default
    if (this.option) {
      this.timelineData.option = this.option
      this.timelineData.option.onMove = item => { this.$emit('item-move', item)}
    }
    this.timelineData.items = this.items
    this.timelineData.groups = this.groups

    this.timelineData.option.start = this.start
    this.timelineData.option.end = this.end
    this.initTimeline()
  }
}

</script>