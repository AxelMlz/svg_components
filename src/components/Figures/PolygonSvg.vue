<template>
  <polygon :points="calculateTriangle(drawing, imageWidth, imageHeight)" :fill="getFillColor(drawing)"
    :stroke="getStrokeColor(drawing)" :stroke-width="(drawing.strokeWidth === 0) ? 1 : drawing.strokeWidth + '%'"
    :opacity="drawing.alpha / 255" :transform="'rotate(' + drawing.angle + ' ' +
      drawing.centerX * imageWidth / 100 +
      ' ' +
      drawing.centerY * imageHeight / 100 +
      ')'
      " />
</template>

<script>
export default {
  name: 'PolygonSvg',
  props: {
    drawing: Object,
    imageWidth: Number,
    imageHeight: Number,
  },
  methods: {
    getFillColor: function (drawing) {
      if (drawing.style === "fill") {
        const color = drawing.color;
        const r = (color >> 16) & 0xff;
        const g = (color >> 8) & 0xff;
        const b = color & 0xff;
        return `rgb(${r}, ${g}, ${b})`;
      }
      return "#00000000";
    },
    getStrokeColor: function (drawing) {
      if (drawing.style === "stroke" || drawing.style === "line") {
        const color = drawing.color;
        const r = (color >> 16) & 0xff;
        const g = (color >> 8) & 0xff;
        const b = color & 0xff;
        return `rgb(${r}, ${g}, ${b})`;
      }
      return "#00000000";
    },
    calculateTriangle: function (drawing, imageWidth, imageHeight) {

      const ax = drawing.centerX * imageWidth / 100;
      const ay = drawing.centerY * imageHeight / 100 - (drawing.height * imageHeight / 100) / 2;

      const bx = drawing.centerX * imageWidth / 100 + (drawing.width * imageWidth / 100) / 2;
      const by = drawing.centerY * imageHeight / 100 + (drawing.height * imageHeight / 100) / 2;

      const cx = drawing.centerX * imageWidth / 100 - (drawing.width * imageWidth / 100) / 2;
      const cy = drawing.centerY * imageHeight / 100 + (drawing.height * imageHeight / 100) / 2;

      return `${ax} ${ay}, ${bx} ${by}, ${cx} ${cy}`;
    },
  }
}
</script>