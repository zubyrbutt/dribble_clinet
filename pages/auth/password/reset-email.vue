<template>
  <section class="authentication">
    <div class="auth-body">
      <h1 class="text-uppercase fw-500 mb-4 text-center font-22">
        Reset Password
      </h1>
      <form class="auth-form" @submit.prevent="submit">
<alert-success :form="form">
  {{status}}
</alert-success>
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

        <div class="mt-4 mb-4 clearfix">

            Back to login page
            <nuxt-link :to="{name: 'login'}">Login</nuxt-link>

        </div>
        <div class="text-right">
          <button :disabled="form.busy" type="submit" class="btn btn-primary">
            <span v-if="form.busy">
              <i class="fas fa-spinner fa-spin"></i>
            </span>
            Resend
          </button>
        </div>

      </form>
    </div>
  </section>
</template>

<script>
  export default {

    data() {
      return {
        status: '',
        form: this.$vform({
          email: '',
        })
      }
    },
    methods: {
      submit() {
this.form.post(
  `/password/email`
).then(res => {
  this.status = res.data.status
  this.form.reset()
})
      }
    }
  }
</script>
