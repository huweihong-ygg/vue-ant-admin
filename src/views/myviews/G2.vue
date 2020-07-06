<template>
  <div>
    <div class="header">G2</div>
    <div id="container"></div>
    <div id="container2"></div>
  </div>
</template>

<script>
import { Chart, Util } from '@antv/g2'
import { registerShape } from '@antv/g2'

export default {
  mounted() {
    this.g2()
    this.g21()
  },
  methods: {
    g21() {
      const data = [
        { type: '分类一', value: 27 },
        { type: '分类二', value: 25 },
        { type: '分类三', value: 18 },
        { type: '分类四', value: 15 },
        { type: '分类五', value: 10 },
        { type: 'Other', value: 5 }
      ]

      let max = 0
      data.forEach(function(obj) {
        if (obj.value > max) {
          max = obj.value
        }
      })

      // 自定义 other 的图形，增加两条线
      registerShape('interval', 'slice-shape', {
        draw(cfg, container) {
          const points = cfg.points
          const origin = cfg.data
          const percent = origin.value / max
          const xWidth = points[2].x - points[1].x
          const width = xWidth * percent
          let path = []
          path.push(['M', points[0].x, points[0].y])
          path.push(['L', points[1].x, points[1].y])
          path.push(['L', points[0].x + width, points[2].y])
          path.push(['L', points[0].x + width, points[3].y])
          path.push('Z')
          path = this.parsePath(path)
          return container.addShape('path', {
            attrs: {
              fill: cfg.color,
              path
            }
          })
        }
      })

      const chart = new Chart({
        container: 'container2',
        autoFit: true,
        height: 500
      })

      chart.coordinate('theta', {
        radius: 0.8
      })

      chart.data(data)

      chart.tooltip({
        showTitle: false,
        showMarkers: false
      })

      chart
        .interval()
        .adjust('stack')
        .position('value')
        .color('type')
        .shape('slice-shape')
        .label('type', {
          offset: -130,
          layout: {
            type: 'limit-in-shape'
          }
        })

      chart.interaction('element-active')

      chart.render()
      interval.elements[0].setState('selected', true)

    },
    g2() {
      const data = [
        { item: '事例一', count: 40, percent: 0.4 },
        { item: '事例二', count: 21, percent: 0.21 },
        { item: '事例三', count: 17, percent: 0.17 },
        { item: '事例四', count: 13, percent: 0.13 },
        { item: '事例五', count: 9, percent: 0.09 }
      ]

      const chart = new Chart({
        container: 'container',
        autoFit: true,
        height: 500
      })

      chart.data(data)

      chart.coordinate('theta', {
        radius: 0.85
      })

      chart.scale('percent', {
        formatter: val => {
          val = val * 100 + '%'
          return val
        }
      })
      chart.tooltip({
        showTitle: false,
        showMarkers: false
      })
      chart.axis(false) // 关闭坐标轴
      const interval = chart
        .interval()
        .adjust('stack')
        .position('percent')
        .color('item')
        .label('percent', {
          offset: -40,
          style: {
            textAlign: 'center',
            shadowBlur: 2,
            shadowColor: 'rgba(0, 0, 0, .45)',
            fill: '#fff'
          }
        })
        .tooltip('item*percent', (item, percent) => {
          percent = percent * 100 + '%'
          return {
            name: item,
            value: percent
          }
        })
        .style({
          lineWidth: 1,
          stroke: '#fff'
        })
      chart.interaction('element-single-selected')
      chart.render()

      // 默认选择
      interval.elements[0].setState('selected', true)
    }
  }
}
</script>

<style>
</style>