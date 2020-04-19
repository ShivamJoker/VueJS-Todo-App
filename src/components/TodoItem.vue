<template>
  <md-list class="lists">
    <md-list-item v-for="todo in todos" :key="todo.id">
      <md-checkbox v-model="todo.completed" />
      <span class="md-list-item-text">{{ todo.title }}</span>
      <md-button
        class="md-icon-button md-list-action"
        @click.stop="$emit('del-todo', todo.id)"
      >
        <md-icon>delete</md-icon>
      </md-button>
    </md-list-item>
  </md-list>
</template>



<script>
export default {
  name: "TodoItem",
  props: ["todos"],
};
</script>


<style scoped>
.lists{
    overflow: scroll;
    height: 340px;
}
</style>