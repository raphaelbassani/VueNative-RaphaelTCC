<template>
  
  
  <view class="container">
    
    <Header title="Olá"  />
    <scroll-view>
      <view class='todo-wrapper' v-for='(todo, index) in todos' :key='index'>
        <todo-item
          :todo='todo'
          :selected-index='index'
          :delete-todo='deleteTodo'
        />
      </view>
    </scroll-view>
    <add-todo
      :on-add='addTodo'
    />
   
  </view>
  
  
</template>

<script>
import Header from "./components/Header";
import AddTodo from './src/AddTodo';
import TodoItem from './src/TodoItem';
import { Alert, AsyncStorage } from 'react-native';

export default {
  data() {
    return {
      todos: [],
    };
  },
  components: {
    AddTodo,
    TodoItem,
    Header,
  },
  methods: {
    addTodo: async function(todo){
      const search = this.todos.filter(todos => todos.task === todo.task);

      if (search.length !== 0) {
        Alert.alert("Item já cadastrado");
        return;
      }
      console.log(this.todos)
      await AsyncStorage.setItem(this.todos)
                            
      this.todos.push(todo)
    },
    
    deleteTodo: function(index) {
      Alert.alert(
      "Deseja deletar este item?",
      "",
      [
        {
          text: "Cancelar",
          onPress: () => {
            return;
          },
          style: "cancel"
        },
        {
          text: "Deletar",
          onPress: () => {
            this.todos.splice(index, 1)
          },
        }
      ],
      { cancelable: false }
    );
    },
  }
}
</script>
>
 
<style>
.container {
  background-color:white;
  flex: 1;
  padding-left: 20;
  padding-right: 20;
  padding-bottom: 40;
  padding-top: 60px;
}
.todo-wrapper {

  background-color: #ffffff;
  justify-content: space-between;
  align-items: center;
  flex-direction: row;
  padding: 10;
  border-radius: 5;
}
</style>
