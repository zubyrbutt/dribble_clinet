<template>
  <section class="authentication">
    <div class="auth-body">
      <h1 class="text-uppercase fw-500 mb-4 text-center font-22">
        Resend Verification Email
      </h1>
      <form class="auth-form" @submit.prevent="submit">
        <alert-error v-if="form.errors.has('message')" :form="form">
{{form.errors.get('message')}}
        </alert-error>
<alert-success :form="form">
  Verification email send successfully
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
        <div class="text-right">
          <button :disabled="form.busy" type="submit" class="btn btn-primary">
            <span v-if="form.busy">
              <i class="fas fa-spinner fa-spin"></i>
            </span>
            Send</button>
        </div>

      </form>
    </div>
  </section>
</template>

<script>
  export default {
    data(){
      return{
        form:this.$vform({
          email: ''
        })

      }
    },
    methods:{
      submit(){
this.form.post(`/verification/resend`)
        .then(res => this.form.reset())
        .catch(e => console.log(e))
      }
    }
  }
</script>
