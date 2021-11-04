<template>
<KeyboardAvoidingView
    keyboardVerticalOffset=0,
    behavior=padding,
    enabled=true,
    class="" 
    >
<view>
  <view class="divider"/>
  <view class="text-input-container">
    <view class="text-input-wrapper">
      <text-input placeholder="Novo item" v-model="newTodo"/>
    </view>
    <touchable-opacity :on-press="addTodo" class='add-button'>
        <image :source='addIcon' class='image-style'/>
      </touchable-opacity>
  </view>
</view>
 </KeyboardAvoidingView>
</template>

<script>

import addIcon from '../assets/edit_icon.png';
import { KeyboardAvoidingView } from 'react-native';
export default {
  data: function() {
    return {
      newTodo: '',
      addIcon,
      KeyboardAvoidingView,
    };
  },
  props: {
    onAdd: Function
  },
  methods: {
    addTodo: function() {
      let todo = {
        task: this.newTodo,
        isCompleted: false,
        edited: false
      }
      this.onAdd(todo)
      this.newTodo = ''
    },
  }
}
</script>
 
<style>
.keyboard {
  flex: 1;
}
.divider {
  border-bottom-color: #505050;
  border-bottom-width: 1px;
  opacity: .3;
  margin-top: 10px;
  margin-bottom: 10px;
}
.image-style { 
  height: 15;
  width: 15;
}
.add-button {
  padding-top: 10;
  padding-bottom: 5;
}
.text-color-primary {
  color: rgba(0, 0, 0, 0.767);
}
.text-input-wrapper {
  flex: 1;
  justify-content: center;
  padding: 10
}
.text-input-container {
  margin-horizontal: 15;
  flex-direction: row;
  padding-bottom: 20
}
</style>
