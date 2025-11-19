<script setup>
import { ref, reactive } from 'vue'

const tasks = [
  { id: 'maze', name: 'Regular Maze', folder: 'maze' },
  { id: 'graph', name: 'Irregular Maze', folder: 'irregular_maze' },
  { id: 'maze3d', name: 'Maze 3D', folder: 'maze3d' },
  { id: 'sokoban', name: 'Sokoban', folder: 'sokoban' },
  { id: 'trapfield', name: 'Trap Field', folder: 'trapfield' }
]

const models = [
  { id: 'sora-2', name: 'Sora 2', file: 'sora-2.mp4' },
  { id: 'veo3_1', name: 'Veo 3.1', file: 'veo3_1.mp4' },
  { id: 'veo3_1-pro', name: 'Veo 3.1 Pro', file: 'veo3_1-pro.mp4' },
  { id: 'kling-v1', name: 'Kling 2.1', file: 'kling-v1.mp4' },
  { id: 'wan2.2', name: 'Wan2.2', file: 'wan2.2_baseline.mp4' },
  { id: 'wan2.1', name: 'Wan2.5', file: 'wan2.5.mp4' },
  { id: 'wan-r1', name: 'Wan R1', file: 'wanr1.mp4' },
  { id: 'hunyuan', name: 'HunyuanVideo', file: 'doubao-seedance-1-0-pro-250528.mp4' },
  { id: 'cogvideo', name: 'MiniMax', file: 'MiniMax-Hailuo-2_3.mp4' }
]

const difficulties = ['easy', 'medium', 'hard']

const taskDifficulties = reactive({})
tasks.forEach(task => {
  taskDifficulties[task.id] = 'easy'
})

const getVideoPath = (taskId, modelFile) => {
  const task = tasks.find(t => t.id === taskId)
  const taskFolder = task?.folder || 'irregular_maze'
  const difficulty = taskDifficulties[taskId] || 'easy'
  return `/VRBench_Web/video_pre/${taskFolder}/${difficulty}/${modelFile}`
}

const setTaskDifficulty = (taskId, difficulty) => {
  taskDifficulties[taskId] = difficulty
}
</script>

<template>
  <div class="case-demonstration">
    <h1 class="section-title">Case Demonstration: Structural Reasoning & Search</h1>

    <div class="task-rows">
      <div
        v-for="task in tasks"
        :key="task.id"
        class="task-row"
      >
        <div class="task-header">
          <div class="task-label">{{ task.name }}</div>
          <div class="task-difficulty-selector">
            <button
              v-for="diff in difficulties"
              :key="diff"
              :class="{ active: taskDifficulties[task.id] === diff }"
              @click="setTaskDifficulty(task.id, diff)"
              class="task-diff-btn">
              {{ diff.charAt(0).toUpperCase() + diff.slice(1) }}
            </button>
          </div>
        </div>

        <div class="video-grid">
          <div
            v-for="model in models"
            :key="`${task.id}-${model.id}`"
            class="video-card"
          >
            <div class="model-name">{{ model.name }}</div>
            <div class="video-wrapper">
              <video
                :key="`${task.id}-${model.id}-${taskDifficulties[task.id]}`"
                :src="getVideoPath(task.id, model.file)"
                controls
                preload="metadata"
                class="video-player"
              >
                Your browser does not support the video tag.
              </video>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.case-demonstration {
  padding: 80px 40px;
  max-width: 1400px;
  margin: 0 auto;
  background: #ffffff;
}

.section-title {
  font-size: 32px;
  font-weight: 700;
  color: #000000;
  text-align: center;
  margin-bottom: 50px;
  letter-spacing: -0.5px;
}

.task-rows {
  display: flex;
  flex-direction: column;
  gap: 32px;
}

.task-row {
  background: linear-gradient(to bottom, #fafafa 0%, #fafafa 85px, #ffffff 85px);
  border-radius: 16px;
  padding: 0;
  box-shadow: 0 2px 12px rgba(0, 0, 0, 0.06);
  border: 1px solid #e8e8ed;
  overflow: hidden;
  transition: all 0.3s ease;
}

.task-row:hover {
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
  transform: translateY(-2px);
}

.task-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 20px 24px;
  background: transparent;
  border-bottom: 1px solid #e8e8ed;
}

.task-label {
  font-size: 22px;
  font-weight: 700;
  color: #1d1d1f;
  text-align: left;
  letter-spacing: -0.3px;
}

.task-difficulty-selector {
  display: flex;
  gap: 6px;
}

.task-diff-btn {
  padding: 8px 18px;
  border: 1px solid #d1d1d6;
  background: #ffffff;
  color: #1d1d1f;
  font-size: 13px;
  font-weight: 500;
  border-radius: 8px;
  cursor: pointer;
  transition: all 0.2s;
  min-width: 75px;
}

.task-diff-btn:hover {
  background: #f5f5f7;
  border-color: #0071e3;
}

.task-diff-btn.active {
  background: #0071e3;
  color: #fff;
  border-color: #0071e3;
  font-weight: 600;
  box-shadow: 0 2px 8px rgba(0, 113, 227, 0.25);
}

.video-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
  padding: 24px;
  background: #ffffff;
}

.video-card {
  background: #ffffff;
  border-radius: 10px;
  overflow: hidden;
  box-shadow: 0 1px 4px rgba(0, 0, 0, 0.08);
  transition: all 0.25s ease;
  border: 1px solid #e8e8ed;
}

.video-card:hover {
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.12);
  transform: translateY(-3px);
  border-color: #0071e3;
}

.model-name {
  padding: 12px 14px;
  font-size: 13px;
  font-weight: 600;
  color: #1d1d1f;
  text-align: center;
  background: #fafafa;
  border-bottom: 1px solid #e8e8ed;
}

.video-wrapper {
  position: relative;
  width: 100%;
  padding-top: 75%;
  background: #f0f0f0;
  overflow: hidden;
}

.video-player {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: contain;
}

.video-placeholder {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: #f0f0f0;
}

@media (max-width: 1024px) {
  .video-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 768px) {
  .case-demonstration {
    padding: 40px 20px;
  }

  .section-title {
    font-size: 24px;
    margin-bottom: 30px;
  }

  .video-grid {
    grid-template-columns: 1fr;
  }

  .task-header {
    flex-direction: column;
    align-items: flex-start;
    gap: 12px;
  }

  .task-label {
    font-size: 18px;
  }

  .task-difficulty-selector {
    width: 100%;
    justify-content: flex-start;
  }

  .task-diff-btn {
    flex: 1;
  }
}

</style>

