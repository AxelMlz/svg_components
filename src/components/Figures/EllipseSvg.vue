<template>
    <ellipse :rx="abs(drawing.width / 2) + '%'" :ry="abs(drawing.height / 2) + '%'" :cx="drawing.centerX + '%'"
        :cy="drawing.centerY + '%'" :fill="getFillColor(drawing)" :stroke="getStrokeColor(drawing)" :stroke-width="drawing.strokeWidth === 0 ? 1 : drawing.strokeWidth + '%'
            " :opacity="drawing.alpha / 255" :transform="'rotate(' +
        drawing.angle +
        ' ' +
        (drawing.centerX * imageWidth) / 100 +
        ' ' +
        (drawing.centerY * imageHeight) / 100 +
        ')'
        " />
</template>
<script>

export default {
    name: "EllipseSvg",
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
        abs(val) {
            return Math.abs(val);
        },
    }
}
</script>