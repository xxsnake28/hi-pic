<template>
  <div>
    <el-upload
      drag
      action="https://jsonplaceholder.typicode.com/posts/"
      :show-file-list="false"
      :limit="3"
      multiple
    >
      <i class="el-icon-upload"></i>
      <div class="el-upload__text">
        将文件拖到此处，或
        <em>点击上传</em>
      </div>
      <div class="el-upload__tip" slot="tip">只能上传jpg/png文件，且不超过500kb</div>
    </el-upload>
  </div>
</template>

<script>
export default {
  name: 'upload-field',
  data() {
    return {
      isUploading: false
    }
  }
}
</script>
