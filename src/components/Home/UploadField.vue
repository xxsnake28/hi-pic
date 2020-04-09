<template>
  <div class="upload-field">
    <el-upload
      drag
      action="https://sm.ms/api/v2/upload"
      :headers="headers"
      name="smfile"
    >
      <i class="el-icon-upload"></i>
      <div class="el-upload__text">
        将文件拖到此处，或
        <em>点击上传</em>
      </div>
      <div class="el-upload__tip" slot="tip">只能上传jpg/png文件，且不超过500kb</div>
    </el-upload>
    <div class="dashboard-container"></div>
  </div>
</template>

<script>
import Uppy from '@uppy/core'
import Dashboard from '@uppy/dashboard'
import XHRUpload from '@uppy/xhr-upload'
import zhCN from '@uppy/locales/lib/zh_CN'
import '@uppy/core/dist/style.css'
import '@uppy/dashboard/dist/style.css'

export default {
  name: 'upload-field',
  data() {
    return {
      uppy: null,
      headers: {
        'Authorization': 'wNGIYc6gKfCkQuY5U0cfE5czgBl5SsWz'
      }
    }
  },
  mounted() {
    this.initUppy()
  },
  computed: {
    loadingText() {
      return ''
    }
  },
  methods: {
    // 初始化uppy
    initUppy() {
      this.uppy = Uppy({
        debug: false,
        autoProceed: false,
        locale: zhCN,
        restrictions: {
          maxFileSize: 1000000,
          maxNumberOfFiles: 3,
          allowedFileTypes: ['image/*']
        }
      })
      this.uppy.on('file-added', file => {
        this.uppy.setFileMeta(file.id, { format: 'json' })
      })
      this.uppy.on('upload-error', (file, error, response) => {
        console.log('error message:', error)
      })
      this.uppy.on('upload-success', (file, response) => {
        console.log(response)
      })

      this.uppy.use(Dashboard, {
        target: '.dashboard-container',
        inline: true,
        showProgressDetails: true,
        hideProgressAfterFinish: true,
        note: '只允许上传图片, 最多同时上传3张，最大为 1 MB'
      })
      this.uppy.use(XHRUpload, {
        endpoint: 'https://sm.ms/api/v2/upload',
        headers: {
          'Authorization': 'wNGIYc6gKfCkQuY5U0cfE5czgBl5SsWz'
        },
        formatData: 'true',
        fieldName: 'smfile',
        metaFields: ['format']
      })
      // this.uppy.use(XHRUpload, {
      //   endpoint: 'https://upload-endpoint.uppy.io/upload'
      // })
    }
  }
}
</script>
<style lang="stylus" scoped>
.upload-field {
  text-align: center;
}

.dashboard-container {
  display: inline-block;
}
</style>
