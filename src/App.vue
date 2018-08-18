<template>
  <div id="app">
    <color-picker v-model="color" />
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
        color: '',
    }
  }
}
</script>
