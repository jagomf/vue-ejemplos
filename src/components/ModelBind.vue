<template>
  <input @keyup.enter="doEnter" v-model="searchText" />
</template>

<script>
export default {
  name: 'ModelBind',
  data() {
    return {
      searchText: '',
    };
  },
  methods: {
    doEnter() {
      console.log(`Buscando..: ${this.searchText}`);
    },
  },
};
</script>

<style>

</style>
