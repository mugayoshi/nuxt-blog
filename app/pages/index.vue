<template>
  <section class="container">
    <el-card style="flex:1">
      <div slot="header" class="clearfix">
        <span>ログイン</span>
      </div>
      <form>
        <div class="form-cnntent">
          <span>ユーザ ID</span>
          <el-input placeholder="" v-model="formData.id" />
        </div>
        <div class="form-content">
          <el-checkbox v-model="isCreateMode">アカウントを作成する</el-checkbox>
        </div>
        <div class="text-right">
          <el-button type="primary" @click="handleClickSubmit">{{ buttonText }}</el-button>
        </div>
      </form>
    </el-card>
  </section>
</template>

<script>
import { mapActions } from 'vuex'

export default {
  asyncData({ redirect, store }){
    if (store.getters['users']){
      redirect('/posts')
    }
    return {
      isCreateMode: false,
      formData: {
        id: ''
      }
    }
  },
  computed: {
    buttonText() {
      return this.isCreateMode ? '新規登録' : 'ログイン'
    }
  },
  methods: {
    async handleClickSubmit(){
      if (this.isCreateMode) {
        try {
          console.log('trying to sign-up')
          await this.register({...this.formData })
          this.$notify({
            type: 'success',
            title: 'アカウント作成完了',
            message: `${this.formData.id}として登録しました`,
            position: 'bottom-right',
            duration: 1000
          })
          console.log('an account is created!')
          this.$router.push('/posts')
        } catch(e){
          this.$notify.error({
            title: 'アカウント作成失敗',
            message: '既に登録されているか，不正なユーザIDです',
            position: 'bottom-right',
            duration: 1000
          })
          
        }
      } else {
        try {
          console.log('trying to login')
          await this.login({...this.formData})
          this.$notify({
             type: 'success',
            title: 'ログイン成功',
            message: `${this.formData.id}としてログインしました`,
            position: 'bottom-right',
            duration: 1000
          })
          console.log('loging success')
          this.$router.push('/posts')
        } catch (e) {
          this.$notify.error({
            title: 'ログイン作成失敗',
            message: '不正なログインユーザIDです',
            position: 'bottom-right',
            duration: 1000
          })
        }
      }
    },
    ...mapActions(['login', 'register'])
  }
}
</script>

<style scoped>
.form-content {
  margin: 16px 0;
}
</style>
