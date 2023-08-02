<template>
    <line v-if="drawing.type === 'line'" :x1="`${drawing.centerX - drawing.width / 2}%`" :y1="`${drawing.centerY}%`"
        :x2="`${drawing.centerX + drawing.width / 2}%`" :y2="`${drawing.centerY}%`" :stroke="getStrokeColor(drawing)"
        :stroke-width="(drawing.strokeWidth === 0) ? 1 : drawing.strokeWidth + '%'" :opacity="drawing.alpha / 255"
        :angle="`${drawing.angle}`" :transform="'rotate(' + (drawing.angle) + ' ' +
            (drawing.centerX * imageWidth) / 100 +
            ' ' +
            (drawing.centerY * imageHeight) / 100 +
            ')'
            " />
</template>
<script>

export default {
    name: "LineArrowSvg",
    props: {
        drawing: Object,
        imageWidth: Number,
        imageHeight: Number,
    },
    methods: {
        getFillColor: function (drawing) {
            if (drawing.style === "fill" || drawing.style === "arrow") {
                const color = drawing.color;
                const r = (color >> 16) & 0xff;
                const g = (color >> 8) & 0xff;
                const b = color & 0xff;
                return `rgb(${r}, ${g}, ${b})`;
            }
            return "#00000000";
        },
        getStrokeColor: function (drawing) {
            if (drawing.style === "stroke" || drawing.style === "line" || drawing.style === "arrow") {
                const color = drawing.color;
                const r = (color >> 16) & 0xff;
                const g = (color >> 8) & 0xff;
                const b = color & 0xff;
                return `rgb(${r}, ${g}, ${b})`;
            }
            return "#00000000";
        },

        created() {
            console.log(this.drawing)
        }
    }
}
</script>