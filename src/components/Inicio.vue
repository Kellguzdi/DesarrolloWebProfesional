<template>
  <div>    
    <b-link :to="{name:'main'}">Siguiente</b-link>
    <b-breadcrumb router-component-name :items="items"></b-breadcrumb>
  </div>
</template>

<script>
export default {
    data() {
      return {
        items: [
          {
            text: 'Inicio',
            href: '#',
            active:true
          },
          
        ]
      }
    }
}
</script>

<style>

</style>