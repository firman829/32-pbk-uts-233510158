<script>
import ActivityList from './components/ActivityList.vue';

export default {
  name: 'App',
  components: {
    ActivityList,
  },
};
</script>

<template>
  <div id="app" class="app-container">
    <h1>daftar tugas belajar mahasiswa 📚</h1>
    <ActivityList />
  </div>
</template>

<style scoped>
.app-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 2rem;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  background-color: #f2f5f9;
  min-height: 100vh;
}

h1 {
  margin-bottom: 1rem;
  color: #333;
}
</style>
