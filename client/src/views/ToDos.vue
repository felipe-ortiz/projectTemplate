<template>
  <div class="todos">
    <div>Hi from todos</div>

    <div v-for="(todo, index) in mytodos" v-bind:key="index">
      <span>{{ todo.name }}</span>
      <span>{{ todo.duedate }}</span>
    </div>
    <div>
      <div class="buttons">
          <a class="button is-primary" v-on:click="showTodoModal()">Add Todo</a>
      </div>
    </div>
    <Todo
      v-bind:is-showing="showTodo"
      v-on:success="successSignup()"
      v-on:cancel="cancelTodoModal()"
    />
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import { Component } from "vue-property-decorator";
import Todo from "@/components/Todo.vue";

@Component({
  components: {
    Todo
  }
})
export default class ToDos extends Vue {
public showTodo: boolean = false;
  mytodos: ToDo[] = [];

  public showTodoModal() {
    this.showTodo = true;
  }
  public onSuccessTodo() {
    this.showTodo = false;
  }
  public cancelTodoModal() {
    this.showTodo = false;
  }

}

interface ToDo {
  id : number;
  title: String;
  body: String;
  duedate: Date | undefined | String;
  tag : String
  userId: number;
  complete: boolean | Date;
}
</script>

<style scoped>
</style>