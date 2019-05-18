<template>
  <div id="app">
    <button
        type="button"
        @click="toggle = !toggle"
    >
      {{ toggle ? 'Hide' : 'Show' }}
    </button>

    <color-picker
        ref="picker"
        v-if="toggle"
        v-model="color"
    />
  </div>
</template>

<script>
import ColorPicker from './components/ColorPicker.vue'

export default {
  name: 'app',
  components: {
      ColorPicker
  },
  data() {
    return {
        toggle: true,
        color: '',
    }
  }
}
</script>
