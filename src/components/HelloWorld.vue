<template>
  <main>
    <div v-if="handler.isLoading" class="loader"></div>
    <div v-if="handler.isError">{{ errorMessage }}</div>
    <div>{{ todo }}</div>
  </main>
</template>

<script>
export default {
  data() {
    return {
      loading: false,
      error: false,
      handler: {
        isLoading: false,
        isError: false,
      },
      errorMessage: "",
      todo: "",
    };
  },
  async created() {
    this.loading = true;

    try {
      const res = await fetch("https://jsonplaceholder.typicode.com/todos/1");
      this.todo = await res.json();
      this.loading = false;
    } catch (error) {
      console.log(error.message);
      this.handler.isLoading = false;
      this.handler.isError = true;
      this.loading = false;
      this.error = true;
      this.errorMessage = error.message;
    }
  },
};
</script>

<style lang="scss" scoped>
.loader {
  border: 16px solid #f3f3f3;
  border-top: 16px solid #3498db;
  border-radius: 50%;
  width: 36px;
  height: 36px;
  animation: spin 2s linear infinite;
}

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>