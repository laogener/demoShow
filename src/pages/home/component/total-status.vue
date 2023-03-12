<template>
  <div>
      <el-image :src="src">
          <div slot="placeholder">
              加载中<span class="dot">...</span>
          </div>
      </el-image>
  </div>
</template>

<script>
export default {
    data() {
        return {
            src:require('@/assets/image/sy.jpeg')
        }
    }
}
</script>
