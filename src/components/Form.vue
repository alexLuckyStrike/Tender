<template>
  <div>
    <b-form @submit="onSubmit" @reset="onReset" v-if="show">
      <b-form-group
        id="input-group-1"
        label="Email address:"
        label-for="input-1"
        description="We'll never share your email with anyone else."
      >
        <b-form-input
          id="input-1"
          v-model="email"
          placeholder="Enter name"
          :class="{invalid:($v.email.$dirty && !$v.email.required) || ($v.email.$dirty && !$v.email.email)}"
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-2" label="Your Name:" label-for="input-2">
        <b-form-input
          id="input-2"
          v-model="surname"
          placeholder="Enter surname"
        ></b-form-input>
      </b-form-group>
      <!-- <pre>{{$v}}</pre> -->
      <b-button type="submit" variant="primary">Submit</b-button>
      <b-button type="reset" variant="danger">Reset</b-button>
    </b-form>

  </div>
</template>

<script>
import {required} from 'vuelidate/lib/validators';

  export default {
    data() {
      return {
          email: '',
          surname: '',
        show: true
      }
    },
    validations:{
        email:{required},
        surname:{required}    
    },
    methods: {
      onSubmit(event) {
        event.preventDefault()
        if(this.$v.$invalid){
         this.$v.$touch()
         return
        }
      },
      onReset(event) {
        event.preventDefault()
        // Reset our form values
        this.form.email = ''
        this.form.name = ''
        // Trick to reset/clear native browser form validation state
        this.show = false
      }
    }
  }
</script>