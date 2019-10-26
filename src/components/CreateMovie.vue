<template>
  <form @submit="onSubmit">
    <p><label>
      Título <input placeholder="Título" :class="titleClass" v-model="title" />
    </label></p>
    <p><label>
      Imagen <input placeholder="URL imagen" v-model="pic" />
    </label></p>
    <p><label>
      Descripción <input placeholder="Descripción" v-model="description" />
    </label></p>
    <p><label>
      Género <input placeholder="Género" v-model="type" />
    </label></p>
    <button type="submit">Crear</button>
  </form>
</template>

<script>
export default {
  name: 'CreateMovie',
  data() {
    return {
      title: '',
      pic: '',
      description: '',
      type: '',
    };
  },
  computed: {
    titleClass({ title }) {
      const classes = {};
      if (!this.checkLength(title, 3)) {
        classes.error = true;
      }
      return classes;
    },
    picClass({ pic }) {
      const classes = {};
      if (!this.checkLength(pic, 3)) {
        classes.error = true;
      }
      return classes;
    },
    descriptionClass({ description }) {
      const classes = {};
      if (!this.checkLength(description, 3)) {
        classes.error = true;
      }
      return classes;
    },
    typeClass({ type }) {
      const classes = {};
      if (!this.checkLength(type, 3)) {
        classes.error = true;
      }
      return classes;
    },
  },
  methods: {
    checkLength(text, minLength) {
      return text.length >= minLength;
    },
    onSubmit() {
      this.$emit('movie-add', {
        title: this.title, description: this.description, type: this.type, pic: this.pic,
      });
    },
  },
};
</script>

<style scoped>
.error {
  background-color: lightcoral;
}
</style>
