<template>
  <v-card>
    <v-card-text>
      <v-card-title style="font-size: 24 px ;">เข้าสู่ระบบ</v-card-title>
        <v-form
          ref="loginForm"
          v-model="valid"
          lazy-validation
        >
          <v-text-field
            v-model="username"
            :counter="20"
            :rules="nameRules"
            label="ชื่อผู้ใช้งาน"
            placeholder="ชื่อผู้ใช้งาน"
            required
            outlined
          ></v-text-field>

          <v-text-field
            v-model="password"
            :rules="passwordRules"
            label="รหัสผ่าน"
            placeholder="รหัสผ่าน"
            required
            outlined
          ></v-text-field>

          <v-btn
            :disabled="!valid"
            color="success"
            class="mr-4"
            @click="Login()"
            block
          >
            เข้าสู่ระบบ
          </v-btn>
        </v-form>
    </v-card-text>
  </v-card>
  
</template>

<script>
export default {
  data: () => ({
      valid: true,
      username: '',
      nameRules: [
        v => !!v || 'กรุณากรอกชื่อผู้ใช้งาน',
        v => (v && v.length <= 20) || 'ชื่อผู้ใช้ห้ามเกิน 20 ตัวอักษร',
      ],
      password: '',
      passwordRules: [
        v => !!v || 'กรุณากรอกรหัสผ่าน',
        
      ],
      id: 0,
      accountItem:[],
    }),

    methods: {
      async Login() {
        if (this.$refs.loginForm.validate(true)) {
          var validateAccount = await this.axios.get(
            'localhost:9000/account?username='+this.username+ '&password='+this.password)
          console.log('validateAccount ===> ' ,validateAccount)
          // this.accountItem = account.data
          // localStorage.setItem('username' , this.name)
          // this.$EventBus.$emit('getUsername')
          // this.$router.push('/')
        }
      }
    }
}
</script>

<style>

</style>