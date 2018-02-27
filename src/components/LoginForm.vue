<template>
  <div class="container">
    <form action="" class="login-form has-shadow">
      <h1 class="form-title">Login</h1>
      <div v-for="field in fields" :key="field.name" class="field-container">
        <label class="form-label" :for="field.name">{{field.label}} <span v-if="isRequired(field.validations)" class="required-indicator">*</span></label>
        <input  v-validate="field.validations" class="form-input" type="text" :name="field.name" v-model="postObject[field.name]">
         <p class="error-tag" v-show="errors.has(field.name)">{{errors.first(field.name)}}</p>
      </div>
      <div class="button-holder">
        <button @click="guardar" type="button" class="button button-save">Guardar</button>
        <button @click="cancelar" type="button" class="button button-cancel">Cancelar</button>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: "LoginForm",
  data() {
    return {
      postObject: [],
      fields: [
        {
          name: "nombre",
          label: "nombre",
          validations: { required: true, alpha: true }
        },
        {
          name: "apellido",
          label: "apellido",
          validations: { required: true, alpha: true }
        },
        {
          name: "edad",
          label: "edad",
          validations: { required: true, numeric: true, between: [1, 120] }
        },
        {
          name: "email",
          label: "email",
          validations: { required: true, email: true }
        }
      ]
    };
  },
  methods: {
    isRequired(validations) {
      return validations.hasOwnProperty("required");
    },
    guardar() {
      this.$validator.validateAll().then(result => {
        if (result) {
          alert("Usuario guardado satisfactoriamente");
        }
      });
    },
    cancelar() {
      this.postObject = [];
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="sass" scoped>

.container
  margin-top: 30px
  text-align: center
  padding-top: 150px
  padding-bottom: 120px
  .login-form
    background-color: #fff
    padding: 30px
    max-width: 33%
    margin-left: 33%
    margin-right: auto
    border-radius: 5px
    min-height: 500px
    &:after 
      content: ""
      background: url('../assets/background.png')
      background-size: cover
      opacity: 0.1
      top: 0
      left: 0
      bottom: 0
      right: 0
      position: absolute
      z-index: -1   
.field-container
  display: flex
  flex-direction: column
  margin-bottom: 5px

.form-label
  font-size: 20px
  font-weight: 300
  color: #224
  text-transform: capitalize
.form-input
  height: 24px
  font-size: 20px
  border-radius: 5px
  border: 1px solid #d7dbe7
.form-title
  font-size: 32px
  border-bottom: 1px solid #224
  margin-bottom: 20px
  font-weight: 700
  color: #224
.button-holder
  margin-top: 60px
.button-save
  color: white
  background-color: #345

.required-indicator
  color: red

.error-tag
  color: red
  font-size: 12px

</style>
