<template>
  <div class="container">
    <div class="canvas"></div>
    <div
      v-show="settingsPanelVisible"
      ref="settings-panel"
      class="settings-panel"
    ></div>
  </div>
</template>

<script>
import * as d3 from 'd3';

export default {
  name: 'app-canvas',

  data() {
    return {
      settingsPanelVisible: false,

      rectangle: {
        width: 70,
        height: 70,
      },
      circle: {
        r: 30,
      },
    };
  },

  methods: {
    renderCanvas() {
      const context = this;

      const svgContainer = d3.select('.canvas')
        .append('svg')
        .attr('width', '100%')
        .attr('height', '100%')
        .on('click', function () { // eslint-disable-line
          context.settingsPanelVisible = false;
        });

      const rect = svgContainer.append('rect')
        .attr('x', 10)
        .attr('y', 10)
        .attr('fill', '#fff')
        .attr('stroke', '#000')
        .attr('stroke-width', 2)
        .attr('width', this.rectangle.width)
        .attr('height', this.rectangle.height)
        .on('click', function () { // eslint-disable-line
          d3.event.stopPropagation();
          // const mouse = d3.mouse(this);
          const settingsPanel = context.$refs['settings-panel'];
          const { x, y, width } = d3.event.originalTarget.attributes;
          // console.log(mouse);
          // console.log(d3.event.originalTarget.attributes);
          // console.log(context.$refs);
          context.settingsPanelVisible = true;
          settingsPanel.style.top = `${y.nodeValue}px`;
          settingsPanel.style.left = `${+x.nodeValue + +width.nodeValue + 10}px`;
        });

      const circle = svgContainer.append('circle')
        .attr('cx', this.rectangle.width / 2 + 10)
        .attr('cy', 180)
        .attr('fill', '#fff')
        .attr('stroke', '#000')
        .attr('stroke-width', 2)
        .attr('r', this.circle.r)
        .on('click', function () { // eslint-disable-line
          d3.event.stopPropagation();
          // const mouse = d3.mouse(this);
          const settingsPanel = context.$refs['settings-panel'];
          const { cx, cy, r } = d3.event.originalTarget.attributes;
          // console.log(mouse);
          // console.log(context.$refs);
          // console.log(d3.event.originalTarget.attributes);
          // console.log(cx.nodeValue, cy.nodeValue, r.nodeValue);
          context.settingsPanelVisible = true;
          settingsPanel.style.top = `${cy.nodeValue - +r.nodeValue}px`;
          settingsPanel.style.left = `${+cx.nodeValue + +r.nodeValue + 10}px`;
        });

      // const line = svgContainer.append('line')
      //   .style('stroke', 'black')
      //   .attr('x1', this.rectangle.width / 2 + 10)
      //   .attr('y1', this.rectangle.height / 2 + 10)
      //   .attr('x2', this.rectangle.width / 2 + 10)
      //   .attr('y2', 180 + this.circle.r / 2 + 10);

      const dragHandler = d3.drag()
        .on('drag', function () {
          if (this.nodeName === 'rect') {
            d3.select(this)
              .attr('x', d3.event.x)
              .attr('y', d3.event.y);

            //  line.attr('x1', d3.event.x + context.rectangle.width / 2);
            //  line.attr('y1', d3.event.y + context.rectangle.height / 2);
          } else if (this.nodeName === 'circle') {
            d3.select(this)
              .attr('cx', d3.event.x)
              .attr('cy', d3.event.y);

            //  line.attr('x2', d3.event.x);
            //  line.attr('y2', d3.event.y);
          }
        });

      dragHandler(rect);
      dragHandler(circle);
    },

    renderSettingsPanel() {
      const svgContainer = d3.select('.settings-panel')
        .append('svg')
        .attr('width', 40)
        .attr('height', 120);

      svgContainer.append('rect')
        .attr('x', 5)
        .attr('y', 5)
        .attr('fill', '#fff')
        .attr('stroke', '#000')
        .attr('width', 30)
        .attr('height', 30);

      svgContainer.append('circle')
        .attr('cx', 20)
        .attr('cy', 60)
        .attr('fill', '#fff')
        .attr('stroke', '#000')
        .attr('r', 15);

      svgContainer.append('line')
        .style('stroke', 'black')
        .attr('x1', 30)
        .attr('y1', 90)
        .attr('x2', 5)
        .attr('y2', 110);
    },
  },

  mounted() {
    this.renderCanvas();
    this.renderSettingsPanel();
  },
};
</script>
