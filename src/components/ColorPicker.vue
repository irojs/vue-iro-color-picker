<template>
    <div ref="picker"></div>
</template>

<script>
  import iro from '@jaames/iro';

  export default {
    props: {
      value: {
        type: String,
        default: '#ffffff',
      },
      width: {
        type: Number,
        default: 300,
      },
      height: {
        type: Number,
        default: 300,
      },
      handleSvg: {
        type: String,
        default: null,
      },
      handleOrigin: {
        type: Object,
        default() {
          return {
            x: 0,
            y: 0,
          };
        },
      },
      padding: {
        type: Number,
        default: 6,
      },
      handleRadius: {
        type: Number,
        default: 8,
      },
      sliderMargin: {
        type: Number,
        default: 24,
      },
      sliderHeight: {
        type: Number,
        default: undefined,
      },
      borderWidth: {
        type: Number,
        default: 0,
      },
      borderColor: {
        type: String,
        default: '#ffffff',
      },
      display: {
        type: String,
        default: 'block',
      },
      layout: {
        type: String,
        default: 'block',
      },
      wheelAngle: {
        type: Number,
        default: 0,
      },
      wheelDirection: {
        type: String,
        default: 'anticlockwise',
      },
      wheelLightness: {
        type: Boolean,
        default: true,
      },
      css: {
        type: Object,
        default: () => {},
      },
    },
    data() {
      return {
        colorPicker: null,
      };
    },
    methods: {
      onInput(color) {
        this.$emit('input', color.hexString);
      },
      onColorChange(color, changes) {
        this.$emit('color:change', {
          color,
          changes,
        });
      },
      onColorInit(color, changes) {
        this.$emit('color:init', {
          color,
          changes,
        });
      },
      onInputChange(color, changes) {
        this.$emit('input:change', {
          color,
          changes,
        });
      },
      onInputStart(color) {
        this.$emit('input:start', {
          color,
        });
      },
      onInputMove(color) {
        this.$emit('input:move', {
          color
        });
      },
      onInputEnd(color) {
        this.$emit('input:end', {
          color
        });
      },
      onMount(colorPicker) {
        this.$emit('mount', {
          colorPicker,
        });
      },
    },
    mounted() {
      this.colorPicker = new iro.ColorPicker(this.$refs.picker, {
        width: this.width,
        height: this.height,
        handleSvg: this.handleSvg,
        color: this.value,
        padding: this.padding,
        layout: this.layout,
        display: this.display,
        css: this.css,
        wheelDirection: this.wheelDirection,
        wheelAngle: this.wheelAngle,
        wheelLightness: this.wheelLightness,
        handleOrigin: this.handleOrigin,
        handleRadius: this.handleRadius,
        sliderMargin: this.sliderMargin,
        sliderHeight: this.sliderHeight,
        borderWidth: this.borderWidth,
        borderColor: this.borderColor,
      });

      this.colorPicker.on('input:end', this.onInput);
      this.colorPicker.on('color:change', this.onColorChange);
      this.colorPicker.on('color:init', this.onColorInit);
      this.colorPicker.on('input:change', this.onInputChange);
      this.colorPicker.on('input:start', this.onInputStart);
      this.colorPicker.on('input:move', this.onInputMove);
      this.colorPicker.on('input:end', this.onInputEnd);
      this.colorPicker.on('mount', this.onMount);
    },
    beforeUnmount() {
      this.colorPicker.off('input:end', this.onInput);
      this.colorPicker.off('color:change', this.onColorChange);
      this.colorPicker.off('color:init', this.onColorInit);
      this.colorPicker.off('input:change', this.onInputChange);
      this.colorPicker.off('input:start', this.onInputStart);
      this.colorPicker.off('input:move', this.onInputMove);
      this.colorPicker.off('input:end', this.onInputEnd);
      this.colorPicker.off('mount', this.onMount);
    },
    watch: {
      value(newValue) {
        if (this.colorPicker.color) {
          this.colorPicker.color.hexString = newValue;
        }
      },
    },
  }
</script>
