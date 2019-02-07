<template>
  <modal v-bind:is-showing="isShowing" title="Todo" success-button="Confirm" v-on:success="success" v-on:cancel="cancel">
    <form v-on:submit.prevent="onSubmit">
      <p v-if="error" class="is-danger">
        {{ error }}
      </p>
      <div class="field">
        <label class="label">Title</label>
        <div class="control">
          <input class="input" type="text" placeholder="title" v-model="todo.title"/>
        </div>
      </div>
      <div class="field">
        <label class="label">Todo</label>
        <div class="control">
          <input class="input" type="text" placeholder="todo" v-model="todo.todo"/>
        </div>
      </div>
      <div class="field">
        <label class="label">Due Date</label>
        <div class="control">
          <input class="input" type="text" placeholder="date" v-model="todo.duedate"/>
        </div>
      </div>
      <div class="field">
        <label class="label">Tag</label>
        <div class="control">
          <input class="input" type="text" placeholder="tag" v-model="todo.tag"/>
        </div>
      </div>
      <div class="field">
        <label class="label">Complete</label>
        <div class="control">
          <input class="input" type="text" placeholder="date" v-model="todo.duedate"/>
        </div>
      </div>
    </form>
  </modal>
</template>



<script lang="ts">
import axios, { AxiosResponse } from "axios";
import { APIConfig } from "../utils/api.utils";
import { Component, Prop, Vue } from "vue-property-decorator";
import Modal from "./Modal.vue";
import { iUser } from "../models/user.interface";

@Component({
  components: { Modal }
})
export default class Todo extends Vue {
  @Prop(Boolean) isShowing: boolean = false;
  todo: TodoForm = {
    title: "",
    body: "",
    duedate: "",
    tag: "",
    complete: undefined
  };
  error: string | boolean = false;

  success() {
    debugger;
    this.error = false;
    // this.signup.firstName = "done";
    console.log("hello");
    axios
      .post(APIConfig.buildUrl("/todo"), {
        ...this.todo
      })
      .then((response: AxiosResponse<iUser>) => {
        this.$emit("success");
      })
      .catch((errorResponse: any) => {
        debugger;
        this.error = errorResponse.response.data.reason;
      });
  }

  cancel() {
    this.$emit("cancel");
  }
}

export interface TodoForm {
  title: String;
  body: String;
  duedate: Date | undefined | String;
  tag : String
  complete: boolean | Date | undefined;
}
</script>
