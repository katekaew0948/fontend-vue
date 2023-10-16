<template>
  <v-app>
    <v-app-bar
      app
      color="#F0CF6D"
      light
    >
      <div class="d-flex align-center">
        COMART
      </div>

      <v-spacer></v-spacer>

      <v-btn
        text
        @click="goToHome()"
      >
        หน้าหลัก
      </v-btn>

      <v-btn
        text
        @click="goToContent()"
      >
        หน้าจัดการร้าน
      </v-btn>

      <v-btn
        text
        @click="goToLogin()"
      >
        เข้าสู่ระบบ
      </v-btn>
    </v-app-bar>

    <v-main>
      <router-view/>
    </v-main>
  </v-app>
</template>

<script>

export default {
  name: 'App',

  data: () => ({
    //
  }),

  methods : {
    goToLogin() {
      this.$router.push({path: '/login'}).catch(() => {})
    } ,

    goToManage() {
      this.$router.push( {path: '/manageTable'} ).catch(() => {})
    },

    goToHome(){
      this.$router.push( {path: '/'} ).catch(() => {})
    },
    goToContent(){
      this.$router.push( {path: '/content'} ).catch(() => {})
    }
  }
}
</script>
