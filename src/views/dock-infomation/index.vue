<template>
  <div class="app-container documentation-container">
    <el-form ref="form" :model="form" label-width="120px">
      <el-form-item label="商户appID">
        <el-input v-model="form.appID" :disabled="true" />
      </el-form-item>
      <el-form-item label="回调地址">
        <el-input v-model="form.returnUrl" placeholder="http://www.test.com/returnUrl" />
      </el-form-item>
      <el-form-item label="通知地址">
        <el-input v-model="form.notifyUrl" placeholder="http://www.test.com/notifyUrl" />
      </el-form-item>
      <el-form-item label="签名方式">
        <el-select v-model="form.signType" placeholder="请选择签名方式">
          <el-option label="ECC" value="ecc" />
          <el-option label="MD5" value="md5" />
        </el-select>
      </el-form-item>
      <el-form-item label="商户密钥">
        <el-input v-model="form.appSecretKey" placeholder="选择ecc时填入ecc 公钥" />
      </el-form-item>
      <el-form-item label="ip白名单开关">
        <el-switch v-model="form.ipWhiteSwitch" />
      </el-form-item>
      <el-form-item label="白名单配置">
        <el-input v-model="form.desc" type="textarea" :disabled="!form.ipWhiteConfig" placeholder="多个ip使用英文的状态下用 , 分开" />
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click="onSubmit">立即创建</el-button>
        <el-button>取消</el-button>
      </el-form-item>
    </el-form>
  </div>
</template>

<script>
export default {
  name: 'DockInfomation',
  data() {
    return {
      form: {
        appID: '',
        appSecretKey: '',
        returnUrl: '',
        notifyUrl: '',
        ipWhiteSwitch: false,
        ipWhiteConfig: '',
        signType: 'md5'
      }
    }
  },
  mounted() {
    this.$store.dispatch('user/getDockInfo').then(data => {
      this.form = { ...data }
    }).catch(() => {
      this.$store.dispatch('user/logout')
    })
  },
  methods: {
    onSubmit() {
      console.log('submit!')
    }
  }
}
</script>

<style lang="scss" scoped>

</style>
