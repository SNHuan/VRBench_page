<script lang="ts" setup>
import { ElIcon } from 'element-plus'
import { Document, Files, DataAnalysis } from '@element-plus/icons-vue'

// Logo path (set to '' to hide)
const logo = '/VRBench_Web/logo.png'

// Title configuration
const titleMain = 'VR-Bench'
const titleRest =
  ": The First Evaluation of Video Models' Reasoning Abilities through Maze-Solving Tasks"
const titleColor = '#000000'
const titleSupp = ''
const titleSuppColor = '#42B883'

// Button color
const btnColor = '#444444'

// Authors (name, homepage, affiliation flags)
const authors = [
  { name: 'Cheng Yang', icon: '', homepage: '', addressFlag: '1' },
  { name: 'Haiyuan Wan', icon: '', homepage: '', addressFlag: '2,3' },
  { name: 'Yiran Peng', icon: '', homepage: '', addressFlag: '1' },
  { name: 'Xin Cheng', icon: '', homepage: '', addressFlag: '4' },
  { name: 'Zhaoyang Yu', icon: '', homepage: '', addressFlag: '1' },
  { name: 'Jiayi Zhang', icon: '', homepage: '', addressFlag: '1,8' },
  { name: 'Junchi Yu', icon: '', homepage: '', addressFlag: '5*' },
  { name: 'Xinlei Yu', icon: '', homepage: '', addressFlag: '6' },
  { name: 'Xiawu Zheng', icon: '', homepage: '', addressFlag: '7' },
  { name: 'Dongzhan Zhou', icon: '', homepage: '', addressFlag: '3' },
  { name: 'Chenglin Wu', icon: '', homepage: '', addressFlag: '1\u2020' },
]

// Affiliations
const addresses = [
  { addressFlag: '1', name: 'DeepWisdom', icon: '', homepage: '' },
  { addressFlag: '2', name: 'Tsinghua University', icon: '', homepage: '' },
  { addressFlag: '3', name: 'Shanghai Artificial Intelligence Laboratory', icon: '', homepage: '' },
  { addressFlag: '4', name: 'Renmin University of China', icon: '', homepage: '' },
  { addressFlag: '5', name: 'University of Oxford', icon: '', homepage: '' },
  { addressFlag: '6', name: 'National University of Singapore', icon: '', homepage: '' },
  { addressFlag: '7', name: 'Xiamen University', icon: '', homepage: '' },
  {
    addressFlag: '8',
    name: 'Hong Kong University of Science and Technology (GuangZhou)',
    icon: '',
    homepage: '',
  },
]

// Equal contribution and corresponding author note
const conAndCorresponding =
  '# Equal Contribution. * Corresponding Author.'

// Emphasis lines (empty for now, no extra block)
const emphases: string[] = []

// Resource buttons
const buttons = [
  { disabled: true, name: 'Paper', component: Document },
  { disabled: true, name: 'Chinese Version', component: Document },
  {
    disabled: false,
    name: 'Code',
    link: 'https://github.com/ImYangC7/VR-Bench',
    component: Files,
  },
  {
    disabled: false,
    name: 'Dataset',
    component: DataAnalysis,
  },
]
</script>

<template>
  <div>
    <!-- Logo -->
    <el-row v-if="logo" justify="center" style="margin-top: 20px">
      <el-image :src="logo" class="logo" fit="contain" />
    </el-row>

    <!-- Title -->
    <el-row justify="center">
      <el-col :span="20">
        <h1 class="paper-title">
          <span v-if="titleMain" class="title-gradient">{{ titleMain }}</span>
          <span v-if="titleRest" :style="{ color: titleColor }"> {{ titleRest }}</span>
          <span v-if="titleSupp" :style="{ color: titleSuppColor }"> {{ titleSupp }}</span>
        </h1>
      </el-col>
    </el-row>

    <!-- Authors -->
    <el-row justify="center">
      <a
        v-for="author in authors"
        :key="author.name"
        :href="author.homepage || 'javascript:void(0);'"
      >
        <el-button class="title-button" type="primary" text>
          <el-avatar
            v-if="author.icon"
            :size="40"
            :src="author.icon"
            class="author-avatar"
          />
          <span class="author">
            {{ author.name
            }}<sup v-if="author.addressFlag" class="name_sup">{{ author.addressFlag }}</sup>
          </span>
        </el-button>
      </a>
    </el-row>

    <!-- Affiliations -->
    <el-row justify="center">
      <a
        v-for="address in addresses"
        :key="address.name"
        :href="address.homepage || 'javascript:void(0);'"
      >
        <el-button class="title-button" type="primary" text>
          <span class="address">
            <sup v-if="address.addressFlag" class="address_sup">{{ address.addressFlag }}</sup>
            {{ address.name }}
          </span>
        </el-button>
      </a>
    </el-row>

    <!-- Equal contribution / corresponding note -->
    <el-row v-if="conAndCorresponding" justify="center" class="con-cor">
      <span class="con-cor-text">{{ conAndCorresponding }}</span>
    </el-row>
    <el-row justify="center" class="con-cor-logo">
      <el-image src="/VRBench_Web/logo_metagpt.png" class="con-logo" fit="contain" />
    </el-row>

    <!-- Emphasis block (currently empty) -->
    <el-row
      v-for="emphasis in emphases"
      :key="emphasis"
      justify="center"
      class="emphasis"
    >
      {{ emphasis }}
    </el-row>

    <!-- Resource buttons -->
    <el-row justify="center" style="margin-bottom: 20px">
      <el-col :span="20">
        <el-row justify="center">
          <a
            v-for="button in buttons"
            :key="button.name"
            :href="button.link || 'javascript:void(0);'"
          >
            <el-button
              class="guidance-button"
              size="default"
              :color="btnColor"
              :disabled="button.disabled"
              round
            >
              <el-icon :size="18">
                <component :is="button.component" />
              </el-icon>
              <span class="btn-text">{{ button.name }}</span>
            </el-button>
          </a>
        </el-row>
      </el-col>
    </el-row>
  </div>
</template>

<style scoped>
/* Title font and layout */
.paper-title {
  font-family: 'MyFont', Verdana, sans-serif;
  letter-spacing: 2px;
  font-size: 42px;
  margin: 32px;
  text-align: center;
}

/* VR-Bench gradient text */
.title-gradient {
  background: linear-gradient(90deg, #2f88ff 0%, #6c42ff 100%);
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
}

/* Author and affiliation buttons */
.title-button {
  margin: 10px 3px;
}

.title-button:hover {
  margin: 10px 8px;
}

/* Resource buttons */
.guidance-button {
  margin: 8px 5px;
  box-shadow: #d8d8d8 1px 1px 1px 1px;
}

/* Author text: bolder and more prominent */
.author {
  font-family: 'MyFont', Verdana, sans-serif;
  font-size: 20px;
  font-weight: 600;
  margin-left: 3px;
}

/* Superscript for authors */
.name_sup {
  font-family: 'MyFont', Verdana, sans-serif;
  color: #606266;
  margin-left: 3px;
}

/* Affiliation text: different, lighter font */
.address {
  font-family: Arial, sans-serif;
  font-size: 16px;
  font-weight: 400;
}

/* Superscript for affiliations */
.address_sup {
  color: #606266;
  margin-right: 1px;
}

/* Contribution note */
.con-cor {
  font-family: Arial, sans-serif;
  font-size: 14px;
  margin: 18px 0;
  text-align: center;
}

.con-cor-text {
  font-style: italic;
}

.con-cor-logo {
  margin-bottom: 10px;
}

.con-logo {
  max-width: 260px;
  width: 60%;
}

/* Emphasis lines */
.emphasis {
  color: chocolate;
  font-weight: bold;
  margin: 8px;
  font-size: 22px;
  text-align: center;
}

/* Resource button text */
.btn-text {
  font-size: 18px;
  color: #ffffff;
}

/* Logo display */
.logo {
  max-width: 200px;
  width: auto;
  height: auto;
  margin-top: 40px;
}

/* Link styles */
a:-webkit-any-link {
  text-decoration: none;
}

a:hover {
  color: inherit;
  border-bottom: none;
}

a {
  text-decoration: none;
  color: inherit;
}
</style>
