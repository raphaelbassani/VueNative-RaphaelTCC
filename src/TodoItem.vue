<template>
  <view class='todo-wrapper'>
    <text v-bind:class="'text-todo-task'">
      {{todo.task}}
    </text>
    <view class="task-input-wrapper" v-if="todo.edited">
      <text-input placeholder='Enter Task' v-model='editedTask'/>
    </view>
    <view class='todo-button-wrapper' v-if="todo.edited">
      <touchable-opacity :on-press="checkIconPress" class='done-button'>
        <image :source='checkIcon' class='image-style'/>
      </touchable-opacity>
      <touchable-opacity v-bind:on-press="cancelIconPress" class='done-button'>
        <image :source='crossIcon' class='image-style'/>
      </touchable-opacity>
    </view>
    <view class='todo-button-wrapper' v-if="!todo.edited">
      <touchable-opacity :on-press="deleteIconPress">
        <image :source='crossIcon' class='image-style'/>
      </touchable-opacity>
    </view>
  </view>
</template>

<script>

import crossIcon from '../assets/delete_icon.png';

export default {
  data: function() {
    return {
      editedTask: this.todo.task,
      crossIcon,
    };
  },
  props: {
    todo: Object,
    selectedIndex: Number,
    editTodo: Function,
    deleteTodo: Function,
    cancelEdit: Function,
    toggleTaskStatus: Function,
    editPressed: Function
  },
  methods: {
    editIconPress: function() {
      this.editPressed(this.selectedIndex)
    },
    checkIconPress: function() {
      if (this.editedTask !== '')
        this.editTodo(this.selectedIndex, this.editedTask)
      else {
        this.editedTask = this.todo.task
        this.cancelEdit(this.selectedIndex)
      }
    },
    cancelIconPress: function() {
      this.cancelEdit(this.selectedIndex)
    },
    handleTaskPressed: function() {
      this.toggleTaskStatus(this.selectedIndex)
    },
    deleteIconPress: function(index) {
      this.deleteTodo(this.selectedIndex)
    },
  }
}
</script>
>
 
<style>
.todo-button-wrapper {
  flex-direction: row
}
.image-style {
  height: 20;
  width: 20;
}
.text-todo-task {
  color:#505050;
}

.todo-wrapper {
  margin-top: 15px;
  margin-bottom: 15px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-direction: row;
  flex: 1;
}
</style>
