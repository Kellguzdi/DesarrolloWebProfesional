<template>
  <div>
    <b-form @submit="checkForm" @reset="onReset" method="post" v-if="show">
        <p v-if="errors.length">
    <b>Por favor, corrija el(los) siguiente(s) error(es):</b>
    <ul>
      <li v-for="error in form.errors">{{ error }}</li>
    </ul>
  </p>
      <b-form-group id="group-1" label="Nombre completo" label-for="name">
        <b-form-input
          id="name"
          v-model="form.name"
          type="text"
          placeholder="Enter you name"
          required
        ></b-form-input>
      </b-form-group>

      <b-form-group id="group-2" label="Direccion" label-for="dir">
        <b-form-input
          id="dir"
          v-model="form.dir"
          type="text"
          placeholder="Enter you direction"
          required
        ></b-form-input>
      </b-form-group>

      <b-form-group id="group-3" label="Fecha de nacimiento" label-for="date">
        <b-form-input
          id="date"
          v-model="form.date"
          type="date"
          placeholder="Enter you birthday"
          required
        ></b-form-input>
      </b-form-group>

      <b-form-group id="group-4" label="Correo electronico" label-for="email">
        <b-form-input
          id="email"
          v-model="form.email"
          type="text"
          placeholder="Enter you email"
          required
        ></b-form-input>
      </b-form-group>

      <b-form-group id="group-5" label="Numero telefonico" label-for="phone">
        <b-form-input
          id="phone"
          v-model="form.phone"
          type="number"
          placeholder="Enter you numero"
          required
        ></b-form-input>
      </b-form-group>

      <b-form-group id="group-6" label="imagen" label-for="img">
        <b-form-input
          id="img"
          v-model="form.img"
          type="text"
          placeholder="Enter you img"
          required
        ></b-form-input>
      </b-form-group>

      <b-button type="submit" variant="primary">Submit</b-button>
      <b-button type="reset" variant="danger">Reset</b-button>
    </b-form>
    <b-card class="mt-3" header="Form Data Result">
      <pre class="m-0">{{ form }}</pre>
    </b-card>
  </div>
</template>

<script>
export default {
  data() {
    return {
      form: {
        errors: [],
        name: "",
        dir: "",
        date: "",
        email: "",
        phone: 0,
        img: "",
      },
      show: true,
    };
  },
  methods: {
    checkForm: function (e) {
      e.preventDefault();
    },
  },
};
</script>

<style>
</style>