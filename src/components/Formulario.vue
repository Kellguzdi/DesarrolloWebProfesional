<template>
  <div>
    <div>
      <b-alert show variant="danger" v-if="errors.length">
        <ul>
          <li v-for="error in errors" :key="error">{{ error }}</li>
        </ul>
      </b-alert>
    </div>
    <b-form @submit="checkForm" @reset="onReset" method="post" novalidate="true" v-if="show">
      
        <b-form-group id="group-1" label="Nombre " label-for="name">
        <b-form-input id="name" v-model="form.name" type="text" placeholder="Enter you name" required></b-form-input>
      </b-form-group>
      <b-form-group id="group-1.1" label="Apellido Paterno" label-for="lastname">
        <b-form-input id="lastname" v-model="form.lastname" type="text" placeholder="Enter you lastname" required></b-form-input>
      </b-form-group>
      <b-form-group id="group-1.2" label="Apellido Materno" label-for="middlename">
        <b-form-input id="middlename" v-model="form.middlename" type="text" placeholder="Enter you middlename" required></b-form-input>
      </b-form-group>
      
      

      <b-form-group id="group-2" label="Direccion" label-for="dir">
        <b-form-input id="dir" v-model="form.dir" type="text" placeholder="Enter you direction" required></b-form-input>
      </b-form-group>

      <b-form-group id="group-3" label="Fecha de nacimiento" label-for="date">
        <b-form-input id="date" v-model="form.date" type="date" placeholder="Enter you birthday" required></b-form-input>
      </b-form-group>

      <b-form-group id="group-4" label="Correo electronico" label-for="email">
        <b-form-input id="email" v-model="form.email" type="text" placeholder="Enter you email" required></b-form-input>
      </b-form-group>

      <b-form-group id="group-5" label="Numero telefonico" label-for="phone">
        <b-form-input id="phone" v-model="form.phone" type="number" placeholder="Enter you numero"
          required></b-form-input>
      </b-form-group>

      <b-form-group id="group-6" label="Selecciona una imagen" label-for="img">
        <b-form-file id="img" v-model="form.img" plain></b-form-file>
      </b-form-group>

      <b-button type="submit" variant="primary">Submit</b-button>
      <b-button type="reset" variant="danger">Reset</b-button>
    </b-form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      form: {        
        name: '',
        lastname:'',
        middlename:'',
        dir: '',
        date: '',
        email: '',
        phone: '',
        img: ''
      },
      errors:[],
      show: true
    }
  },
  methods: {
    checkForm(e) {
      
      this.errors = []

      if (!this.form.name && !this.form.lastname) {
        this.errors.push('Nombre y apellido requeridos.')
      }else if(!this.validName(this.form.name)&&!this.validName(this.form.lastname)) {
        this.errors.push('Don´t write special characters.')
      }
      if (!this.form.dir) {
        this.errors.push('Direccion requerida.')
      }else if (!this.validDir(this.form.dir)){
        this.errors.push('Don´t write special characters to direction.')
      }
      if (!this.form.date) {
        this.errors.push('Fecha de nacimiento requerida.')
      }else if (!this.validDate(this.form.date)){
        
      }
      if (!this.form.email) {
        this.errors.push('Email requerido.')
      } else if (!this.validEmail(this.form.email)) {
        this.errors.push('Valid email required.')
      }
      if (!this.form.phone) {
        this.errors.push('Telefono requerido.')
      } else if (!this.validPhone(this.form.phone)) {
        this.errors.push('Must be 10 digits.')
      }
      if (!this.form.img) {
        this.errors.push('Imagen requerida.')
      }else if (!this.validImg(this.form.img)){
        this.errors.push('Max 3mb.')
      }
      if (!this.errors.length) {        
        alert("formulario enviado")
        return true;
      }
      
      e.preventDefault()
    },
    //validar name que no contenga numeros ni caracteres especiales
    validName: function (name) {
      var re = /^[a-zA-Z\s,'-]+$/;
      return re.test(name);
    },
    validName: function (lastname) {
      var re = /^[a-zA-Z\s,'-]+$/;
      return re.test(lastname);
    },
    validName: function (middlename) {
      var re = /^[a-zA-Z\s,'-]+$/;
      return re.test(middlename);
    },
    //validar direccion que no contenga caracteres especiales
    validDir: function (dir) {
      var re = /^[a-zA-Z0-9\s,'-]+$/;
      return re.test(dir);
    },
    validDate: function (date){
      var fecha = new Date(date);
      var hoy = new Date();
      var edad = parseInt((hoy -fecha)/365/24/60/60/1000);
      if(edad < 18){
        this.errors.push('You must be 18 years old.')
      }
      if(edad > 100){
        this.errors.push('You must be less than 100 years old.')
      }
      if(edad < 0){
        this.errors.push('You must be born.')
      }
      if(fecha >= hoy){
        this.errors.push('The future not exist.')
      }
    },
    validEmail: function (email) {
      var re = /\S+@\S+\.\S+/
      return re.test(email)
    },
    validPhone: function (phone) {
      var re = /^\d{10}$/
      return re.test(phone)
    },
    validImg: function (img) {
      var re = /(?:\.([^.]+))?$/
      return re.test(img)
    },
    onReset(evt) {
      evt.preventDefault()    
      this.form.name = ''
      this.form.dir = ''
      this.form.date = ''
      this.form.email = ''
      this.form.phone = ''
      this.form.img = ''    
      this.show = false
      this.$nextTick(() => {
        this.show = true
      })
    }
  }
};
</script>

<style></style>