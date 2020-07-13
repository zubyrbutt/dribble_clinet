<template>
  <section class="authentication">
    <div class="auth-body">
      <h1 class="text-uppercase fw-500 mb-4 text-center font-22">Register</h1>
      <form class="auth-form" @submit.prevent="submit">

        <alert-success :form="form">
          We have send you verification email.. Please verify your email
        </alert-success>
        <div class="form-group" >
          <input v-model.trim="form.name" name="name" :class="{ 'is-invalid': form.errors.has('name')}" class="form-control" type="text" placeholder="Full Name">
        <has-error :form="form" field="name"></has-error>
        </div>
        <div class="form-group">
          <input
            v-model.trim="form.username"
            name="username"
            type="text"
            class="form-control"
            placeholder="Username"
            :class="{ 'is-invalid': form.errors.has('password') }"
          >
          <has-error :form="form" field="username" ></has-error>
        </div>
        <div class="form-group">
          <input
            v-model.trim="form.email"
            name="email"
            type="email"
            :class="{'is-invalid': form.errors.has('email')}"
            class="form-control"
            placeholder="Email"
          >
          <has-error :form="form" field="email"></has-error>
        </div>
        <div class="form-group">
          <input
            v-model.trim="form.password"
            :class="{ 'is-invalid': form.errors.has('password')}"
            name="password"
            class="form-control"
            type="password"
            placeholder="Password"
          >
          <has-error :form="form" field="password"></has-error>
        </div>
        <div class="form-group">
          <input
            :class="{ 'is-invalid': form.errors.has('password_confirmation')}"
            v-model.trim="form.password_confirmation"
            name="password_confirmation"
            class="form-control"
            type="password"
            placeholder="Confirm Password"
          >
          <has-error :form="form" field="password_confirmation"></has-error>
        </div>

        <div class="text-right">
          <button :disabled="form.busy" type="submit" class="btn btn-primary">
            <span v-if="form.busy">
              <i class="fas fa-spinner fa-spin"></i>
            </span>
            Register</button>
        </div>
        <p class="font-14 fw-400 text-center mt-4">
          Already have an account?
          <nuxt-link :to="{name: 'login'}" class="color-blue">Login</nuxt-link>

        </p>
      </form>
    </div>
  </section>
</template>

<script>
  export default {
    data() {
      return {
        form: this.$vform({
          username: '',
          name: '',
          email: '',
          password: '',
          password_confirmation: ''
        })
      };
    },
    methods: {
      submit() {
        this.form.post(`/register`)
        .then(res =>{
          this.form.reset()
          console.log(res)
        }).catch( error => {
          console.log(error)
        })
      }
    }
  };
</script>


<style>

</style>

