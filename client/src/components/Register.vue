<template>
  <v-layout column>
    <v-layout row wrap>
      <v-flex xs6 offset-xs3>
        <panel title ="Register">
          <form
            name="tab-tracker-form"
            autocomplete="off">
            <v-text-field
              v-model="email"
              label="E-mail"
              required
            ></v-text-field>
            <v-text-field
              v-model="password"
              :counter="32"
              label="Password"
              required
              type="password"
              autocomplete="new-password"
            ></v-text-field>
          </form>
          <br>
          <div class="error" v-html="error" />
          <br>
          <v-btn
            dark
            class="blue"
            @click="register">
            Register
          </v-btn>
        </panel>
      </v-flex>
    </v-layout>
  </v-layout>
</template>

<script>
import AuthenticationService from '@/services/AuthenticationService'
import Panel from '@/components/Panel'
export default {
  data () {
    return {
      email: '',
      password: '',
      error: null
    }
  },
  methods: {
    async register () {
      try {
        const response = await AuthenticationService.register({
          email: this.email,
          password: this.password
        })
        this.$store.dispatch('setToken', response.data.token)
        this.$store.dispatch('setUser', response.data.user)
      } catch (error) {
        this.error = error.response.data.error
      }
    }
  },
  components: {
    Panel
  }
}

</script>
<style scoped>

</style>
