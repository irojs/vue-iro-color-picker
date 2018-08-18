<template>
    <div class="color-picker">
        <div id="color-picker"></div>
    </div>
</template>

<script>
  import iro from "@jaames/iro";

  export default {
    props: {
      value: {
        type: String,
        default: '#ffffff',
      },
      width: {
        type: Number,
        default: 320,
      },
      height: {
        type: Number,
        default: 320,
      },
      padding: {
        type: Number,
        default: 6,
      },
      markerRadius: {
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
      anticlockwise: {
        type: Boolean,
        default: false,
      },
      wheelLightness: {
        type: Boolean,
        default: undefined,
      },
      css: {
        type: Object,
        default: () => {},
      },
    },
    data() {
      return {
        colorPicker: null,
        oldValue: this.value,
      }
    },
    mounted() {
      this.colorPicker = new iro.ColorPicker("#color-picker", {
        width: this.width,
        height: this.height,
        color: this.value,
        padding: this.padding,
        markerRadius: this.markerRadius,
        sliderMargin: this.sliderMargin,
        sliderHeight: this.sliderHeight,
        borderWidth: this.borderWidth,
        borderColor: this.borderColor,
        display: this.display,
        anticlockwise: this.anticlockwise,
        wheelLightness: this.wheelLightness,
        css: this.css,
      });

      this.colorPicker.on("color:change", (color) => {
        this.$emit('input', color.hexString);
      });
    },
    watch: {
      value(newValue) {
        if (this.colorPicker.color) {
          this.colorPicker.color.hexString = newValue;
        }
      }
    }
  }
</script>
