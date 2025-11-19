<script setup>
import abstract from '../mds/abstract.mdx';
</script>

<template>
  <div>
    <el-divider />

    <el-row justify="center">
      <el-col :xs="24" :sm="20" :md="16" :lg="12" :xl="12">
        <div class="abstract-card">
          <abstract />
        </div>
      </el-col>
    </el-row>

  </div>
</template>

<style scoped>
.abstract-card {
  margin: 10px 0 30px;
  padding: 24px 32px;
  border-radius: 18px;
  background: #fbfcff;
  box-shadow: 0 10px 30px rgba(15, 23, 42, 0.08);
}

.abstract-card :deep(h1) {
  text-align: center;
  margin-top: 0;
  margin-bottom: 18px;
}

.abstract-card :deep(p) {
  text-align: justify;
  text-justify: inter-word;
  line-height: 1.8;
}

.abstract-card :deep(strong) {
  color: #4f46e5;
  font-weight: 600;
}
</style>
