<template lang="html">

    <div class="row">
        <div class="panel panel default">
          <div class="panel-body">

            <div class="form-group">
              <input type="text" v-model="email" class="form-control" placeholder="Email">
            </div>

            <div class="form-group">
              <input type="password" v-model="password" class="form-control" placeholder="Password">
            </div>

            <button @click="login" class="btn btn-success pull-right">Login</button>
          </div>
        </div>
      </div>
</template>

<script>
export default {
  data() {
    return {
      email: '',
      password: ''
    }
  },
  methods: {
    login() {
      var data = {
        client_id: 2,
        client_secret: 'KYUGpNISTvhxiRN4o1nAV2JYy1nSajQF5UKoLJoM',
        grant_type: 'password',
        username: this.email,
        password: this.password
      }

      this.$http.post("oauth/token", data)
        .then(function(response){
          this.$auth.setToken(response.body.access_token, response.body.expires_in + Date.now())

          this.$router.push("/feed")
        })
    }
  }
}
</script>

<style lang="css">
</style>
