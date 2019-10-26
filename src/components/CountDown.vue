<template>
  <div>Valor dentro del componente: {{current}}</div>
</template>

<script>
export default {
  name: 'count-down',
  props: {
    from: {
      type: Number,
      default: 0,
    },
  },
  model: {
    prop: 'from',
    event: 'tick',
  },
  data() {
    return {
      current: '',
      intervalId: 0,
    };
  },
  mounted() {
    if (this.from > 0) {
      this.current = this.from;
      this.startCount();
    }
  },
  methods: {
    startCount() {
      this.intervalId = setInterval(() => {
        this.current -= 1;
      }, 1000);
    },
  },
  watch: {
    current(newVal) {
      this.$emit('tick', newVal);
      if (newVal === 0) {
        this.$emit('boom', newVal);
        clearInterval(this.intervalId);
      }
    },
  },
};
</script>

<style>

</style>
