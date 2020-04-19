<template>
  <md-list class="lists">
    <transition-group name="list">
      <md-list-item v-for="todo in todos" :key="todo.id" class="list-item">
        <md-checkbox v-model="todo.completed" />
        <span class="md-list-item-text">{{ todo.title }}</span>
        <md-button
          class="md-icon-button md-list-action"
          @click.stop="$emit('del-todo', todo.id)"
        >
          <md-icon>delete</md-icon>
        </md-button>
      </md-list-item>
    </transition-group>
  </md-list>
</template>

<script>
export default {
  name: "TodoItem",
  props: ["todos"],
};
</script>

<style scoped>
.lists {
  overflow: scroll;
  height: 340px;
}

.list-item {
  transition: all 0.3s cubic-bezier(0.25, 0.46, 0.45, 0.94);
}


.list-enter {
  opacity: 0;
  transform: translateY(-30px);
}
.list-leave-to {
  opacity: 0;
  transform: translateX(300px);
}

.list-leave-active {
  position: absolute;
}

</style>
