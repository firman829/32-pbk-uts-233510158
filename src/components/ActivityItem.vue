<script>
  export default {
    props: ['activity'],
    data() {
      return {
        isCompleted: false,
      };
    },
    methods: {
      toggleComplete() {
        this.$emit('toggle-complete', this.activity.id, this.isCompleted);
      },
      removeActivity() {
        this.$emit('remove-activity', this.activity.id);
      },
    },
  };
</script>

<template>
    <div class="activity-item" :class="{ completed: isCompleted }">
      <input type="checkbox" v-model="isCompleted" @change="toggleComplete" />
      <span class="activity-text" :class="{ 'text-completed': isCompleted }">
        {{ activity.text }}
      </span>
      <button class="delete-button" @click="removeActivity">hapus</button>
    </div>
</template>
  
<style scoped>
  .activity-item {
    display: flex;
    align-items: center;
    justify-content: space-between;
    background-color: #ffffff;
    padding: 0.75rem 1rem;
    margin-bottom: 0.5rem;
    border-radius: 8px;
    box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);
    transition: background 0.3s;
  }
  
  .activity-item:hover {
    background-color: #eef3f7;
  }
  
  .activity-text {
    flex-grow: 1;
    margin: 0 1rem;
    font-size: 1rem;
    color: #333;
  }
  
  .text-completed {
    text-decoration: line-through;
    color: #aaa;
  }
  
  .delete-button {
    background-color: transparent;
    border: none;
    cursor: pointer;
    font-size: 1.2rem;
    transition: transform 0.2s;
  }
  
  .delete-button:hover {
    transform: scale(1.2);
  }
</style>
  