<script setup>
import { ref, computed, watch } from 'vue'
import katex from 'katex'
import 'katex/dist/katex.min.css'

const props = defineProps({
  datasets: { type: Array, required: true },
  title: { type: String, default: 'Model Performance Comparison' },
})

const selectedDatasetIndex = ref(0)
const selectedMetrics = ref([])
const selectedDifficulties = ref([])
const selectedGroups = ref([])

watch(selectedDatasetIndex, () => {
  selectedMetrics.value = []
  selectedDifficulties.value = []
  selectedGroups.value = []
})

const currentData = computed(() => props.datasets[selectedDatasetIndex.value]?.data || {})
const currentCaption = computed(() => props.datasets[selectedDatasetIndex.value]?.caption || '')

// 渲染 LaTeX 公式
const renderLatex = (text) => {
  if (!text) return ''

  try {
    // 处理行内公式 $...$
    let result = text.replace(/\$([^\$]+)\$/g, (match, formula) => {
      try {
        return katex.renderToString(formula, { throwOnError: false })
      } catch (e) {
        return match
      }
    })

    // 处理显示公式 $$...$$
    result = result.replace(/\$\$([^\$]+)\$\$/g, (match, formula) => {
      try {
        return katex.renderToString(formula, { displayMode: true, throwOnError: false })
      } catch (e) {
        return match
      }
    })

    return result
  } catch (e) {
    return text
  }
}

const renderedCaption = computed(() => renderLatex(currentCaption.value))

const hasAnyBaseline = computed(() => {
  const mainKey = Object.keys(currentData.value)[0]
  if (!mainKey) return false

  for (const task of Object.keys(currentData.value[mainKey])) {
    const taskData = currentData.value[mainKey][task]
    for (const metric of Object.keys(taskData)) {
      for (const difficulty of Object.keys(taskData[metric])) {
        const cellData = taskData[metric][difficulty]
        if (cellData && cellData.baseline !== null && cellData.baseline !== undefined) {
          return true
        }
      }
    }
  }
  return false
})

const dataType = computed(() => {
  return hasAnyBaseline.value ? 'performance' : 'grouped'
})

// 检查是否所有数据都只有 fine 值（baseline 和 delta 都为 null）
const isOnlyFineData = computed(() => {
  const mainKey = Object.keys(currentData.value)[0]
  if (!mainKey) return false

  for (const task of Object.keys(currentData.value[mainKey])) {
    const taskData = currentData.value[mainKey][task]
    for (const metric of Object.keys(taskData)) {
      for (const difficulty of Object.keys(taskData[metric])) {
        const cellData = taskData[metric][difficulty]
        if (cellData) {
          // 如果有任何 baseline 或 delta 不为 null，则不是纯 fine 数据
          if ((cellData.baseline !== null && cellData.baseline !== undefined) ||
              (cellData.delta !== null && cellData.delta !== undefined)) {
            return false
          }
        }
      }
    }
  }
  return true
})

const allMetrics = computed(() => {
  const mainKey = Object.keys(currentData.value)[0]
  if (!mainKey) return []
  const firstTask = Object.keys(currentData.value[mainKey])[0]
  return firstTask ? Object.keys(currentData.value[mainKey][firstTask]) : []
})

const allDifficulties = computed(() => {
  const mainKey = Object.keys(currentData.value)[0]
  if (!mainKey) return []
  const firstTask = Object.keys(currentData.value[mainKey])[0]
  if (!firstTask) return []
  const firstMetric = allMetrics.value[0]
  return firstMetric ? Object.keys(currentData.value[mainKey][firstTask][firstMetric]) : []
})

const displayedMetrics = computed(() => selectedMetrics.value.length === 0 ? allMetrics.value : selectedMetrics.value)
const displayedDifficulties = computed(() => selectedDifficulties.value.length === 0 ? allDifficulties.value : selectedDifficulties.value)

const allGroups = computed(() => {
  const mainKey = Object.keys(currentData.value)[0]
  if (!mainKey) return []
  const groups = new Set()
  Object.keys(currentData.value[mainKey]).forEach((task) => {
    const parts = task.split('__')
    if (parts.length > 1) groups.add(parts[0])
  })
  return Array.from(groups)
})

const tableData = computed(() => {
  const mainKey = Object.keys(currentData.value)[0]
  if (!mainKey) return []

  if (dataType.value === 'performance') {
    return Object.keys(currentData.value[mainKey])
      .filter((task) => {
        if (selectedGroups.value.length === 0) return true
        const parts = task.split('__')
        const groupName = parts.length > 1 ? parts[0] : 'Other'
        return selectedGroups.value.includes(groupName)
      })
      .map((task) => {
        const taskData = currentData.value[mainKey][task]
        const parts = task.split('__')
        const groupName = parts.length > 1 ? parts[0] : 'Other'
        const modelName = parts.length > 1 ? parts[1] : task
        const row = { task, groupName, modelName, type: 'performance' }
        allMetrics.value.forEach((metric) => {
          allDifficulties.value.forEach((difficulty) => {
            row[`${metric}_${difficulty}`] = taskData[metric]?.[difficulty]
          })
        })
        return row
      })
  } else {
    const rows = []
    const groupedTasks = {}

    Object.keys(currentData.value[mainKey]).forEach((task) => {
      const parts = task.split('__')
      const groupName = parts.length > 1 ? parts[0] : 'Other'
      const modelName = parts.length > 1 ? parts[1] : task

      if (selectedGroups.value.length > 0 && !selectedGroups.value.includes(groupName)) return

      if (!groupedTasks[groupName]) groupedTasks[groupName] = []
      groupedTasks[groupName].push({ task, modelName, groupName })
    })

    Object.keys(groupedTasks).forEach((groupName) => {
      groupedTasks[groupName].forEach((model) => {
        const taskData = currentData.value[mainKey][model.task]
        const row = { task: model.task, modelName: model.modelName, groupName: model.groupName, type: 'grouped' }
        allMetrics.value.forEach((metric) => {
          allDifficulties.value.forEach((difficulty) => {
            row[`${metric}_${difficulty}`] = taskData[metric]?.[difficulty]
          })
        })
        rows.push(row)
      })
    })

    return rows
  }
})

const toggleMetric = (metric) => {
  const index = selectedMetrics.value.indexOf(metric)
  index > -1 ? selectedMetrics.value.splice(index, 1) : selectedMetrics.value.push(metric)
}

const toggleDifficulty = (difficulty) => {
  const index = selectedDifficulties.value.indexOf(difficulty)
  index > -1 ? selectedDifficulties.value.splice(index, 1) : selectedDifficulties.value.push(difficulty)
}

const toggleGroup = (group) => {
  const index = selectedGroups.value.indexOf(group)
  index > -1 ? selectedGroups.value.splice(index, 1) : selectedGroups.value.push(group)
}

const resetFilters = () => {
  selectedMetrics.value = []
  selectedDifficulties.value = []
  selectedGroups.value = []
}

const formatValue = (value) => (value === null || value === undefined) ? '−' : Number(value).toFixed(1)
const formatDelta = (value) => {
  if (value === null || value === undefined) return '(−)'
  const num = Number(value)
  return num > 0 ? `(+${num.toFixed(1)})` : `(${num.toFixed(1)})`
}

const getDeltaClass = (value, metric) => {
  if (value === null || value === undefined) return ''
  const absValue = Math.abs(value)
  if (metric === 'SD') {
    if (value < 0) {
      if (absValue >= 50) return 'delta-excellent'
      if (absValue >= 30) return 'delta-very-good'
      if (absValue >= 10) return 'delta-good'
    } else if (value > 0) {
      if (absValue >= 50) return 'delta-poor'
      if (absValue >= 30) return 'delta-low'
      if (absValue >= 10) return 'delta-medium'
    }
  } else {
    if (value > 0) {
      if (absValue >= 50) return 'delta-excellent'
      if (absValue >= 30) return 'delta-very-good'
      if (absValue >= 10) return 'delta-good'
    } else if (value < 0) {
      if (absValue >= 50) return 'delta-poor'
      if (absValue >= 30) return 'delta-low'
      if (absValue >= 10) return 'delta-medium'
    }
  }
  return 'delta-neutral'
}

const getValueBgClass = (value, metric) => {
  if (value === null || value === undefined) return ''
  const num = Number(value)

  // VLM-Score: 0-5 分数范围（越高越好）
  if (metric === 'VLM-Score') {
    if (num >= 4.0) return 'bg-excellent'
    if (num >= 3.0) return 'bg-very-good'
    if (num >= 2.0) return 'bg-good'
    if (num >= 1.0) return 'bg-medium'
    if (num >= 0.5) return 'bg-low'
    return 'bg-poor'
  }

  // SD: 越小越好
  if (metric === 'SD') {
    if (num <= 10) return 'bg-excellent'
    if (num <= 20) return 'bg-very-good'
    if (num <= 30) return 'bg-good'
    if (num <= 40) return 'bg-medium'
    if (num <= 50) return 'bg-low'
    return 'bg-poor'
  }

  // 其他指标: 0-100 范围（越高越好）
  if (num >= 80) return 'bg-excellent'
  if (num >= 60) return 'bg-very-good'
  if (num >= 40) return 'bg-good'
  if (num >= 20) return 'bg-medium'
  if (num >= 10) return 'bg-low'
  return 'bg-poor'
}
</script>

<template>
  <div class="table-container">
    <el-divider />
    <el-row justify="center">
      <h1 class="section-title">{{ title }}</h1>
    </el-row>

    <div class="chart-wrapper">
      <div class="filters" v-if="datasets.length > 1 || allGroups.length > 0 || allMetrics.length > 0">
      <div class="filter-row" v-if="datasets.length > 1">
        <label>Dataset:</label>
        <button v-for="(dataset, index) in datasets" :key="index"
          :class="{ active: selectedDatasetIndex === index }"
          @click="selectedDatasetIndex = index">
          {{ dataset.name }}
        </button>
      </div>

      <div class="filter-row">
        <div class="filter-group" v-if="allGroups.length > 0">
          <label>Group:</label>
          <button v-for="group in allGroups" :key="group"
            :class="{ active: selectedGroups.includes(group) }"
            @click="toggleGroup(group)">
            {{ group }}
          </button>
        </div>

        <div class="filter-group">
          <label>Metric:</label>
          <button v-for="metric in allMetrics" :key="metric"
            :class="{ active: selectedMetrics.includes(metric) }"
            @click="toggleMetric(metric)">
            {{ metric }}
          </button>
        </div>

        <div class="filter-group">
          <label>Difficulty:</label>
          <button v-for="difficulty in allDifficulties" :key="difficulty"
            :class="{ active: selectedDifficulties.includes(difficulty) }"
            @click="toggleDifficulty(difficulty)">
            {{ difficulty }}
          </button>
        </div>

        <button class="reset-btn" @click="resetFilters">Reset</button>
      </div>
    </div>

    <div class="table-wrapper">
      <table class="data-table">
        <thead>
          <tr>
            <th rowspan="2" class="task-header">{{ dataType === 'performance' ? 'Task' : 'Method' }}</th>
            <th v-for="metric in displayedMetrics" :key="metric" :colspan="displayedDifficulties.length">{{ metric }}</th>
          </tr>
          <tr>
            <template v-for="metric in displayedMetrics" :key="metric">
              <th v-for="difficulty in displayedDifficulties" :key="`${metric}_${difficulty}`">{{ difficulty }}</th>
            </template>
          </tr>
        </thead>
        <tbody>
          <template v-for="(row, index) in tableData" :key="index">
            <tr v-if="(index === 0 || tableData[index - 1].groupName !== row.groupName) && row.groupName && row.groupName !== 'Other'" class="group-row">
              <td :colspan="displayedMetrics.length * displayedDifficulties.length + 1" class="group-header">
                {{ row.groupName }}
              </td>
            </tr>
            <tr>
              <td class="task-cell">{{ row.modelName || row.task }}</td>
              <template v-for="metric in displayedMetrics" :key="metric">
                <td v-for="difficulty in displayedDifficulties" :key="`${metric}_${difficulty}`"
                  :class="[
                    'value-cell',
                    isOnlyFineData && row[`${metric}_${difficulty}`] && row[`${metric}_${difficulty}`].fine !== null
                      ? getValueBgClass(row[`${metric}_${difficulty}`].fine, metric)
                      : ''
                  ]">
                  <template v-if="row[`${metric}_${difficulty}`]">
                    <div v-if="row[`${metric}_${difficulty}`].baseline !== null && row[`${metric}_${difficulty}`].baseline !== undefined"
                         class="baseline-value">
                      {{ formatValue(row[`${metric}_${difficulty}`].baseline) }}
                    </div>
                    <div v-if="row[`${metric}_${difficulty}`].fine !== null && row[`${metric}_${difficulty}`].fine !== undefined"
                         class="main-value">
                      {{ formatValue(row[`${metric}_${difficulty}`].fine) }}
                    </div>
                    <div v-if="row[`${metric}_${difficulty}`].delta !== null && row[`${metric}_${difficulty}`].delta !== undefined"
                         class="delta-value"
                         :class="getDeltaClass(row[`${metric}_${difficulty}`].delta, metric)">
                      {{ formatDelta(row[`${metric}_${difficulty}`].delta) }}
                    </div>
                  </template>
                  <template v-else>
                    <div class="single-value">−</div>
                  </template>
                </td>
              </template>
            </tr>
          </template>
        </tbody>
      </table>
    </div>

    <transition name="caption-fade" mode="out-in">
      <div v-if="currentCaption" :key="selectedDatasetIndex" class="table-caption" v-html="renderedCaption"></div>
    </transition>
    </div>
  </div>
</template>

<style scoped>
.table-container {
  padding: 40px 0;
  width: 100%;
}
.section-title{
  margin-bottom: 28px;
}

/* 整体包裹容器 */
.chart-wrapper {
  background: #ffffff;
  border-radius: 20px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.08);
  padding: 24px;
  overflow: hidden;
  transition: box-shadow 0.3s ease;
}

.chart-wrapper:hover {
  box-shadow: 0 8px 30px rgba(0, 0, 0, 0.12);
}

.filters {
  background: linear-gradient(135deg, #f8f9fa 0%, #f5f5f7 100%);
  padding: 20px 24px;
  border-radius: 12px;
  margin-bottom: 24px;
  display: flex;
  flex-direction: column;
  gap: 14px;
  border: 1px solid #e5e5e7;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.04);
}

.filter-row {
  display: flex;
  align-items: center;
  gap: 12px;
  flex-wrap: wrap;
  padding: 4px 0;
}

.filter-group {
  display: flex;
  align-items: center;
  gap: 10px;
}

.filters label {
  font-size: 13px;
  font-weight: 700;
  color: #0071e3;
  min-width: 70px;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.filters button {
  padding: 8px 16px;
  border: 1.5px solid #d1d1d6;
  background: #fff;
  color: #1d1d1f;
  font-size: 13px;
  font-weight: 500;
  border-radius: 8px;
  cursor: pointer;
  transition: all 0.25s cubic-bezier(0.4, 0, 0.2, 1);
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.05);
}

.filters button:hover {
  background: #f5f5f7;
  border-color: #0071e3;
  transform: translateY(-1px);
  box-shadow: 0 2px 6px rgba(0, 113, 227, 0.15);
}

.filters button.active {
  background: linear-gradient(135deg, #0071e3 0%, #005bb5 100%);
  color: #fff;
  border-color: #0071e3;
  box-shadow: 0 3px 8px rgba(0, 113, 227, 0.3);
  transform: translateY(-1px);
}

.reset-btn {
  margin-left: auto;
  background: linear-gradient(135deg, #ff3b30 0%, #e63027 100%) !important;
  color: #fff !important;
  border-color: #ff3b30 !important;
  font-weight: 600 !important;
}

.reset-btn:hover {
  background: linear-gradient(135deg, #ff2d20 0%, #d62b1f 100%) !important;
  box-shadow: 0 3px 8px rgba(255, 59, 48, 0.3) !important;
}

.table-wrapper {
  overflow-x: auto;
  border: 1px solid #e5e5e7;
  border-radius: 12px;
  background: #fff;
  margin-bottom: 0;
}

.data-table {
  width: 100%;
  border-collapse: collapse;
  font-size: 13px;
}

.data-table thead {
  background: #f5f5f7;
  position: sticky;
  top: 0;
  z-index: 10;
}

.data-table th {
  padding: 12px 16px;
  text-align: center;
  font-weight: 600;
  color: #1d1d1f;
  border: 1px solid #d1d1d6;
}

.task-header {
  min-width: 150px;
  background: #fafafa;
}

.data-table tbody tr {
  border-bottom: 1px solid #e8e8ed;
}

.data-table tbody tr:hover {
  background: #fafafa;
}

.group-row {
  background: #e8e8ed !important;
}

.group-header {
  padding: 10px 16px !important;
  font-weight: 700;
  color: #0071e3;
  text-align: left;
  font-size: 14px;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.task-cell {
  padding: 16px;
  text-align: left;
  font-weight: 600;
  color: #1d1d1f;
  border: 1px solid #e8e8ed;
  min-width: 150px;
}

.value-cell {
  padding: 8px 12px;
  text-align: center;
  border: 1px solid #e8e8ed;
  min-width: 80px;
  vertical-align: middle;
}

.baseline-value {
  font-size: 13px;
  font-weight: 500;
  color: #86868b;
  margin-bottom: 4px;
}

.main-value {
  font-size: 15px;
  font-weight: 700;
  color: #1d1d1f;
  margin-bottom: 4px;
}

.delta-value {
  font-size: 12px;
  font-weight: 500;
  padding: 2px 6px;
  border-radius: 4px;
  display: inline-block;
}

.delta-excellent {
  background: #d4f4dd;
  color: #1e7e34;
}

.delta-very-good {
  background: #e3f9e5;
  color: #28a745;
}

.delta-good {
  background: #f0fdf4;
  color: #34c759;
}

.delta-neutral {
  background: #f5f5f7;
  color: #86868b;
}

.delta-medium {
  background: #fff3e0;
  color: #e65100;
}

.delta-low {
  background: #ffebee;
  color: #c62828;
}

.delta-poor {
  background: #ffcdd2;
  color: #b71c1c;
}

.single-value {
  font-size: 15px;
  font-weight: 600;
  color: #1d1d1f;
}

.bg-excellent {
  background: #d4f4dd !important;
}

.bg-excellent .baseline-value,
.bg-excellent .main-value {
  color: #1e7e34;
  font-weight: 700;
}

.bg-very-good {
  background: #e3f9e5 !important;
}

.bg-very-good .baseline-value,
.bg-very-good .main-value {
  color: #28a745;
  font-weight: 700;
}

.bg-good {
  background: #f0fdf4 !important;
}

.bg-good .baseline-value,
.bg-good .main-value {
  color: #34c759;
  font-weight: 600;
}

.bg-medium {
  background: #fff3e0 !important;
}

.bg-medium .baseline-value,
.bg-medium .main-value {
  color: #e65100;
  font-weight: 600;
}

.bg-low {
  background: #ffebee !important;
}

.bg-low .baseline-value,
.bg-low .main-value {
  color: #c62828;
  font-weight: 600;
}

.bg-poor {
  background: #ffcdd2 !important;
}

.bg-poor .baseline-value,
.bg-poor .main-value {
  color: #b71c1c;
  font-weight: 700;
}

.table-caption {
  margin-top: 24px;
  padding: 20px 24px;
  background: linear-gradient(135deg, #f8f9fa 0%, #f5f5f7 100%);
  border-left: 4px solid #0071e3;
  border-radius: 12px;
  font-size: 13.5px;
  line-height: 1.7;
  color: #1d1d1f;
  border: 1px solid #e5e5e7;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.04);
  position: relative;
  padding-left: 28px;
}

.table-caption::before {
  content: '';
  position: absolute;
  left: 0;
  top: 0;
  bottom: 0;
  width: 4px;
  background: linear-gradient(180deg, #0071e3 0%, #005bb5 100%);
  border-radius: 12px 0 0 12px;
}

.caption-fade-enter-active {
  transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
}

.caption-fade-leave-active {
  transition: all 0.3s cubic-bezier(0.4, 0, 1, 1);
}

.caption-fade-enter-from {
  opacity: 0;
  transform: translateY(15px) scale(0.98);
}

.caption-fade-leave-to {
  opacity: 0;
  transform: translateY(-10px) scale(0.98);
}
</style>