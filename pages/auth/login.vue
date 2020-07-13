<template>
  <section class="authentication">
    <div class="auth-body">
      <h1 class="text-uppercase fw-500 mb-4 text-center font-22">
        Login
      </h1>
      <form class="auth-form" @submit.prevent="submit">

        <div class="form-group">
          <input
            v-model.trim="form.email"
            name="email"
            type="text"
            class="form-control"
            :class="{'is-invalid': form.errors.has('email')}"
            placeholder="Email"
          >
          <has-error :form="form" field="email"></has-error>
        </div>
        <div class="form-group">
          <input
            v-model.trim="form.password"
            name="password"
            :class="{'is-invalid': form.errors.has('password')}"
            class="form-control"
            type="password"
            placeholder="Password"
          >
          <has-error :form="form" field="password"></has-error>
        </div>
        <div class="mt-4 mb-4 clearfix">
         <a href="">Forgot password?</a>

        </div>
        <div class="text-right">
          <button :disabled="form.busy" type="submit" class="btn btn-primary">
            <span v-if="form.busy">
              <i class="fas fa-spinner fa-spin"></i>
            </span>
            Login</button>
        </div>
        <p class="font-14 fw-400 text-center mt-4">
          Don't have an account yet?

          <nuxt-link :to="{name: 'register'}">Create an account</nuxt-link>

        </p>
      </form>
    </div>
  </section>
</template>

<script>
  export default {
data(){
  return{
    form:this.$vform({
      email: '',
      password: ''
    })
  }
},
    methods:{
submit(){
  this.$auth.loginWith('local',{
    data: this.form
  }).then(res =>{
    console.log('res')
  }).catch(errors =>{
    this.form.errors.set(errors.response.data.errors)
  })
}
    }
  }
</script>
