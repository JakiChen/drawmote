<script>
import Button from '@/components/Desktop/Toolbar/Button/Button.vue'

import { getRgbaString, shadeRgbColor } from '@/tools/helpers.js'

import threads from '@/store/vuetamin/threads'

export default {
  name: 'ToolbarButtonColor',
  extends: Button,

  vuetamin: {
    handleColorChange: [threads.BRUSH_COLOR]
  },

  computed: {
    style() {
      if (!this.tool.color) {
        return {}
      }

      return {
        background: this.tool.color.getRgbaString(100),
        color: getRgbaString(shadeRgbColor(this.tool.color.rgb, -0.2), 0.5)
      }
    },

    additionalClasses() {
      return ['toolbar-item--color-' + this.tool.color.name]
    }
  },

  methods: {
    handleColorChange(state) {
      this.isActive = this.tool.color.name === state.brush.color.name
    },

    handleClick() {
      this.$vuetamin.store.mutate('updateBrushColor', this.tool.color)
      this.$track('Toolbar', 'setColor', this.tool.color.name)
    }
  }
}
</script>

<style lang="scss">
.toolbar-item--colors {
  overflow: visible;
  .toolbar-button {
    border-radius: 100%;
    width: 0.75em;
    height: 0.75em;
    @include media('lg') {
      width: 0.5em;
      height: 0.5em;
    }

    &:hover,
    .hover & {
      opacity: 0.75;
    }
  }

  &.toolbar-item--color-black .toolbar-button {
    box-shadow: 0 0 0 1px $alt-color;
  }

  &.active .toolbar-button {
    box-shadow: 0 0px 0px 2px $alt-color-darker,
      0 0px 0px 4px $alt-color-lighter;
  }
}
</style>
