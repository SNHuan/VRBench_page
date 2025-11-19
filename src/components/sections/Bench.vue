<script>
import { use } from 'echarts/core'
import { CanvasRenderer } from 'echarts/renderers'
import { RadarChart } from 'echarts/charts'
import {
  TitleComponent,
  TooltipComponent,
  LegendComponent,
  RadarComponent,
} from 'echarts/components'
import VChart from 'vue-echarts'
import { provide } from 'vue'

use([CanvasRenderer, RadarChart, TitleComponent, TooltipComponent, LegendComponent, RadarComponent])

// Tasks and metrics
const TASKS = ['Base', 'Irreg', 'Trap', '3D', 'Soko']

// Model data (same as create_radial_bar_charts.py)
const MODELS_DATA = {
  'Gemini-2.5-pro': {
    EM: [2.8, 36.1, 13.9, 2.8, 25.0],
    SR: [4.2, 37.5, 13.9, 2.8, 31.9],
    PR: [9.5, 47.9, 57.6, 19.4, 33.8],
    SD: [25.0, 1.9, 0, 0, 1.1],
    Category: 'vlm',
  },
  'GPT-5 high': {
    EM: [13.9, 31.9, 18.1, 0, 23.6],
    SR: [69.4, 33.3, 27.8, 1.4, 34.7],
    PR: [11.8, 43.6, 53.7, 23.7, 35.6],
    SD: [31.0, 2.1, 6.9, 20, 0.5],
    Category: 'vlm',
  },
  'Qwen2.5-VL-7B': {
    EM: [0, 1.3, 0, 0, 1.4],
    SR: [1.4, 6.9, 1.4, 1.4, 2.8],
    PR: [6.5, 12.4, 14.3, 11.3, 7.8],
    SD: [300.0, 26.7, 66.7, 80, 1150.0],
    Category: 'vlm',
  },
  'Veo-3.1-fast': {
    EM: [0, 0, 0, 0, 2.8],
    SR: [40.3, 36.1, 38.9, 48.6, 43.1],
    PR: [20.2, 24.8, 28.2, 13.4, 21.7],
    SD: [195.3, 111.5, 80.7, 33.5, 112.3],
    Category: 'closed',
  },
  'Veo-3.1-pro': {
    EM: [0, 4.2, 1.4, 0, 0],
    SR: [47.2, 36.1, 59.7, 50.0, 37.5],
    PR: [24.6, 33.9, 39.1, 18.0, 21.4],
    SD: [140.7, 94.5, 85.4, 40.1, 141.8],
    Category: 'closed',
  },
  'Sora-2': {
    EM: [1.4, 5.6, 0, 0, 4.2],
    SR: [75.0, 72.2, 83.0, 37.5, 43.1],
    PR: [45.1, 45.7, 46.6, 19.3, 27.4],
    SD: [302.9, 187.0, 145.1, 92.4, 138.7],
    Category: 'closed',
  },
  'Kling-v1': {
    EM: [0, 0, 0, 0, 0],
    SR: [2.8, 0, 1.4, 27.8, 12.5],
    PR: [6.3, 8.8, 10.4, 11.7, 9.0],
    SD: [25.2, 0, 0, 69.7, 356.1],
    Category: 'closed',
  },
  'Seedance-1.0-pro': {
    EM: [0, 2.8, 2.8, 0, 0],
    SR: [75.0, 45.8, 59.7, 77.8, 13.9],
    PR: [12.8, 35.8, 42.7, 23.6, 17.1],
    SD: [162.3, 143.4, 99.1, 84.4, 241.9],
    Category: 'closed',
  },
  'MiniMax-Hailuo-2.3': {
    EM: [0, 1.4, 2.8, 0, 0],
    SR: [68.1, 40.3, 70.8, 55.6, 45.8],
    PR: [23.2, 24.2, 30.3, 20.3, 15.5],
    SD: [464.0, 170.0, 90.9, 50.1, 165.5],
    Category: 'closed',
  },
  'Wan2.5-i2v-preview': {
    EM: [0, 2.8, 4.2, 0, 0],
    SR: [58.3, 26.4, 77.8, 24.5, 22.4],
    PR: [14.3, 21.8, 34.4, 24.5, 17.1],
    SD: [378.4, 281.8, 73.2, 119.9, 278.0],
    Category: 'open',
  },
  'Wan2.2-TI2V-5B': {
    EM: [0, 0, 0, 0, 0],
    SR: [6.9, 12.5, 0, 31.9, 11.1],
    PR: [6.6, 9.1, 7.1, 12.8, 9.2],
    SD: [388.7, 66.1, 0, 5.4, 176.6],
    Category: 'open',
  },
  'Wan-R1': {
    EM: [33.3, 56.9, 38.9, 65.3, 4.2],
    SR: [76.4, 69.4, 100.0, 100.0, 69.4],
    PR: [60.6, 71.6, 79.1, 93.5, 44.3],
    SD: [10.3, 2.4, 3.9, 3.9, 10.2],
    Category: 'ours',
  },
}

// Colors (following create_radial_bar_charts.py)
const VLM_COLORS = ['#08519c', '#3182bd', '#6baed6']
const VIDEO_COLORS = ['#a63603', '#d94801', '#f16913', '#fd8d3c', '#fdae6b', '#fdd0a2', '#fee6ce', '#fff5eb']
const OURS_COLORS = ['#00441b', '#238b45', '#66c2a4']

const MODEL_COLORS = {
  'Gemini-2.5-pro': VLM_COLORS[0],
  'GPT-5 high': VLM_COLORS[1],
  'Qwen2.5-VL-7B': VLM_COLORS[2],
  'Sora-2': VIDEO_COLORS[0],
  'Veo-3.1-pro': VIDEO_COLORS[1],
  'Seedance-1.0-pro': VIDEO_COLORS[2],
  'MiniMax-Hailuo-2.3': VIDEO_COLORS[3],
  'Veo-3.1-fast': VIDEO_COLORS[4],
  'Wan2.5-i2v-preview': VIDEO_COLORS[5],
  'Kling-v1': VIDEO_COLORS[6],
  'Wan2.2-TI2V-5B': VIDEO_COLORS[7],
  'Wan-R1': OURS_COLORS[0],
}

const METRIC_TITLES = {
  EM: 'Exact Match (EM)',
  SR: 'Success Rate (SR)',
  PR: 'Precision Rate (PR)',
  SD: 'Step Deviation (SD)',
}

const METRIC_BUTTON_LABELS = {
  EM: 'Exact Match (EM)',
  SR: 'Success Rate (SR)',
  PR: 'Precision Rate (PR)',
  SD: 'Step Deviation (SD)',
}

function hexToRgba(hex, alpha) {
  const trimmed = hex.replace('#', '')
  const bigint = parseInt(trimmed, 16)
  const r = (bigint >> 16) & 255
  const g = (bigint >> 8) & 255
  const b = bigint & 255
  return `rgba(${r}, ${g}, ${b}, ${alpha})`
}

function buildMetricOption(metricName, config = {}) {
  const { showLegend = true, splitLegendTwoRows = false, titleFontSize = 16, radius = '60%' } =
    config
  const modelNames = Object.keys(MODELS_DATA)

  // Collect log-normalized values similar to _prepare_metric_data
  const logs = {}
  let maxLog = 0

  modelNames.forEach((model) => {
    const rawVals = MODELS_DATA[model][metricName]
    const transformed = rawVals.map((v) => {
      if (metricName === 'SD') {
        const inv = 1.0 / (1.0 + v)
        return Math.log1p(Math.max(0, inv))
      }
      return Math.log1p(Math.max(0, v))
    })
    logs[model] = transformed
    transformed.forEach((lv) => {
      if (lv > maxLog) maxLog = lv
    })
  })

  const normValues = {}
  modelNames.forEach((model) => {
    normValues[model] = logs[model].map((lv) => {
      if (maxLog <= 0) return 0.08
      return Math.max(0.08, lv / maxLog)
    })
  })

  return {
    title: {
      text: METRIC_TITLES[metricName],
      left: 'center',
      textStyle: {
        fontSize: titleFontSize,
        fontWeight: 'bold',
      },
    },
    tooltip: {
      trigger: 'item',
      textStyle: {
        fontSize: 14,
      },
      formatter: (params) => {
        const modelName = params.name
        const rawVals = MODELS_DATA[modelName][metricName]
        const lines = [`<b>${modelName}</b>`]
        for (let i = 0; i < TASKS.length; i += 1) {
          const suffix = metricName === 'SD' ? '' : '%'
          lines.push(`${TASKS[i]}: ${rawVals[i]}${suffix}`)
        }
        return lines.join('<br/>')
      },
    },
    legend: showLegend
      ? splitLegendTwoRows
        ? [
            {
              type: 'plain',
              bottom: 30,
              data: modelNames.slice(0, Math.ceil(modelNames.length / 2)),
              textStyle: {
                fontSize: 14,
              },
            },
            {
              type: 'plain',
              bottom: 0,
              data: modelNames.slice(Math.ceil(modelNames.length / 2)),
              textStyle: {
                fontSize: 14,
              },
            },
          ]
        : {
            type: 'scroll',
            bottom: 0,
            data: modelNames,
            textStyle: {
              fontSize: 14,
            },
          }
      : { show: false },
    radar: {
      indicator: TASKS.map((task) => ({ name: task, max: 1 })),
      radius,
      splitNumber: 4,
      name: {
        textStyle: {
          fontSize: 14,
        },
      },
    },
    series: [
      {
        type: 'radar',
        data: modelNames.map((model) => ({
          name: model,
          value: normValues[model],
          lineStyle: {
            color: MODEL_COLORS[model],
          },
          itemStyle: {
            color: MODEL_COLORS[model],
          },
          areaStyle: {
            color: hexToRgba(MODEL_COLORS[model], 0.15),
          },
        })),
      },
    ],
  }
}

export default {
  components: {
    VChart,
  },
  setup() {
    provide('THEME_KEY', 'light')
  },
  data() {
    return {
      largeOptions: {
        EM: buildMetricOption('EM', {
          showLegend: true,
          splitLegendTwoRows: true,
          titleFontSize: 18,
          radius: '70%',
        }),
        SR: buildMetricOption('SR', {
          showLegend: true,
          splitLegendTwoRows: true,
          titleFontSize: 18,
          radius: '70%',
        }),
        PR: buildMetricOption('PR', {
          showLegend: true,
          splitLegendTwoRows: true,
          titleFontSize: 18,
          radius: '70%',
        }),
        SD: buildMetricOption('SD', {
          showLegend: true,
          splitLegendTwoRows: true,
          titleFontSize: 18,
          radius: '70%',
        }),
      },
      selectedMetric: 'EM',
      metricLabels: METRIC_BUTTON_LABELS,
    }
  },
  methods: {
    onSmallClick(metric) {
      this.selectedMetric = metric
    },
  },
}
</script>

<template>
  <div>
    <el-divider />

    <el-row justify="center">
      <h1 class="section-title">VR-Bench Evaluation</h1>
    </el-row>

    <!-- Metric selector buttons -->
    <el-row justify="center" style="margin-top: 10px">
      <el-col :xs="24" :sm="22" :md="20" :lg="16" :xl="12" style="text-align: center">
        <el-button-group>
          <el-button
            v-for="metric in ['EM', 'SR', 'PR', 'SD']"
            :key="metric"
            size="small"
            :type="selectedMetric === metric ? 'primary' : 'default'"
            @click="onSmallClick(metric)"
          >
            {{ metricLabels[metric] }}
          </el-button>
        </el-button-group>
      </el-col>
    </el-row>

    <!-- Enlarged chart with shared legend -->
    <el-row justify="center" style="margin-top: 30px">
      <el-col :xs="24" :sm="22" :md="20" :lg="20" :xl="18">
        <v-chart class="radar-chart-large" :option="largeOptions[selectedMetric]" autoresize />
      </el-col>
    </el-row>
  </div>
</template>

<style scoped>
.radar-chart-large {
  height: 850px;
  margin-top: 10px;
}
</style>
