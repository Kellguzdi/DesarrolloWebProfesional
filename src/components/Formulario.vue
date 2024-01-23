<template>
  <div>
    <b-form @submit="checkForm" @reset="onReset" method="post" novalidate="true" v-if="show">

      <b-form-group id="group-2" label="Nombre completo" label-for="name">
        <b-form-input id="name" v-model="form.name" type="text" placeholder="Enter you name" required></b-form-input>
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
        errors:[],
        name: '',
        dir: '',
        date: '',
        email: '',
        phone: '',
        img: ''
      },
      show: true
    }
  },
  methods: {
    checkForm(e) {
      if (this.form.name && this.form.dir && this.form.date && this.form.email && this.form.phone && this.form.img) {
        alert('Formulario enviado')
      }
      this.errors = []

      if (!this.form.name) {
        this.errors.push('Name required.')
      }
      if (!this.form.dir) {
        this.errors.push('Direction required.')
      }
      if (!this.form.date) {
        this.errors.push('Date required.')
      }else if (!this.validDate(this.form.date)){
        this.errors.push('Valid date required.')
      }
      if (!this.form.email) {
        this.errors.push('Email required.')
      } else if (!this.validEmail(this.form.email)) {
        this.errors.push('Valid email required.')
      }
      if (!this.form.phone) {
        this.errors.push('Phone required.')
      } else if (!this.validPhone(this.form.phone)) {
        this.errors.push('Valid phone required.')
      }
      if (!this.form.img) {
        this.errors.push('Image required.')
      }else if (!this.validImg(this.form.img)){
        this.errors.push('Valid image required.')
      }

      e.preventDefault()
    },
    validDate: function (date){
      var fecha = new Date(date);
      var hoy = new Date();
      var edad = parseInt((hoy -fecha)/365/24/60/60/1000);
      if(edad < 18){
        this.errors.push('You must be 18 years old.')
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