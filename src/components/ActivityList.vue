<script>
  import ActivityItem from './ActivityItem.vue';
  
  export default {
    components: {
      ActivityItem,
    },
    data() {
      return {
        activities: [],
        newActivityText: '',
        showCompleted: true,
      };
    },
    computed: {
      filteredActivities() {
        if (this.showCompleted) {
          return this.activities;
        } else {
          return this.activities.filter(activity => !activity.completed);
        }
      },
    },
    methods: {
      addActivity() {
        if (this.newActivityText.trim()) {
          this.activities.push({
            id: Date.now(),
            text: this.newActivityText,
            completed: false,
          });
          this.newActivityText = '';
        }
      },
      removeActivity(id) {
        this.activities = this.activities.filter(activity => activity.id !== id);
      },
      toggleComplete(id, completed) {
        const activity = this.activities.find(activity => activity.id === id);
        if (activity) {
          activity.completed = completed;
        }
      },
      filterActivities() {
        this.showCompleted = !this.showCompleted;
      },
    },
  };
</script>

<template>
    <div class="list-container">
      <div class="input-group">
        <input
          type="text"
          v-model="newActivityText"
          @keyup.enter="addActivity"
          placeholder="tambahkan daftar tugas baru..."
        />
        <button class="add-button" @click="addActivity">➕ tambah</button>
      </div>
  
      <div class="filter-group">
        <button class="filter-button" @click="filterActivities">
          {{ showCompleted ? 'tampilkan daftar tugas aktif' : 'tampilkan semua daftar tugas' }}
        </button>
      </div>
  
      <div class="activities">
        <ActivityItem
          v-for="activity in filteredActivities"
          :key="activity.id"
          :activity="activity"
          @remove-activity="removeActivity"
          @toggle-complete="toggleComplete"
        />
      </div>
    </div>
</template>
  
<style scoped>
  .list-container {
    width: 100%;
    max-width: 600px;
  }
  
  .input-group {
    display: flex;
    gap: 0.5rem;
    margin-bottom: 1rem;
  }
  
  .input-group input {
    flex-grow: 1;
    padding: 0.6rem;
    border: 1px solid #ccc;
    border-radius: 8px;
    font-size: 1rem;
  }
  
  .add-button {
    background-color: #4caf50;
    color: white;
    border: none;
    padding: 0.6rem 1rem;
    border-radius: 8px;
    cursor: pointer;
    transition: background 0.3s;
  }
  
  .add-button:hover {
    background-color: #45a049;
  }
  
  .filter-group {
    margin-bottom: 1rem;
    text-align: right;
  }
  
  .filter-button {
    background-color: #2196f3;
    color: white;
    border: none;
    padding: 0.6rem 1rem;
    border-radius: 8px;
    cursor: pointer;
    transition: background 0.3s;
  }
  
  .filter-button:hover {
    background-color: #1e88e5;
  }
  
  .activities {
    display: flex;
    flex-direction: column;
  }
</style>
  