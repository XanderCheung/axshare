<template>
  <el-upload
    class="upload-demo"
    drag
    :action="uploadSetting.upload_url"
    :data="uploadSetting"
    :on-exceed="onExceed"
    :on-success="onSuccess"
    :on-error="onError"
  >
    <i class="el-icon-upload" />
    <div class="el-upload__text">将文件拖到此处，或<em>点击上传</em></div>
    <div slot="tip" class="el-upload__tip">只能上传zip/rar文件</div>
  </el-upload>
</template>

<script>
import { getQiNiuToken } from '@/api/qiniu'
import { alertMessage } from '@/utils/alert-message'

export default {
  name: 'UploadAttachment',
  data() {
    return {
      uploadSetting: {
        token: '',
        upload_url: ''
      },
      fileHash: ''
    }
  },
  computed: {

  },
  created() {
    this.getToken()
  },
  methods: {
    onExceed() {
      alertMessage({ type: 'error', content: '只能上传一个文件，请先删除已选择的文件！' })
    },
    onSuccess(response, file, fileList) {
      this.fileHash = response.hash
      this.$emit('attachment-hash', this.fileHash)
    },
    onError(err, file, fileList) {
      alertMessage({ type: 'error', content: err })
    },
    getToken() {
      getQiNiuToken().then(response => {
        this.uploadSetting = response.data
      })
    }
  }
}
</script>
