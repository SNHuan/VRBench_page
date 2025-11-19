<script setup>
</script>

<template>
  <div>
    <el-divider />

    <el-row justify="center">
      <h1 class="section-title">Maze Variations</h1>
    </el-row>

    <el-row justify="center">
      <el-col :xs="24" :sm="22" :md="20" :lg="18" :xl="16">
        <el-container class="maze-container">
          <el-image
            class="maze-image"
            src="/VRBench_Web/domain_vary.jpg"
            fit="contain"
          />
        </el-container>
      </el-col>
    </el-row>
  </div>
</template>

<style scoped>
.maze-container {
  margin: 20px 0 0 0;
}

.maze-image {
  width: 65%;
  margin: 0 auto;
  border-radius: 12px;
  box-shadow: 0 10px 30px rgba(15, 23, 42, 0.08);
}
</style>
