<template>
  <div id="container">
    <p>{{ message }}</p>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      message: 'Loading...'
    };
  },
  mounted() {
    this.fetchMessage();
  },
  methods: {
    async fetchMessage() {
      try {
        if (import.meta.env.VITE_DEBUG === 'true') {
          console.log("import.meta.env.VITE_API_URL: ", import.meta.env.VITE_API_URL);
        }
        const response = await fetch(import.meta.env.VITE_API_URL);
        const data = await response.json();
        this.message = data.message;
      } catch (error) {
        console.error('Error fetching message:', error);
        this.message = 'Error loading message';
      }
    }
  }
};
</script>

<style>
#app {
  text-align: center;
  margin: 0px auto;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>

<style scoped>
#container {
  width: 100%;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  font-size: 32px;
}
</style>