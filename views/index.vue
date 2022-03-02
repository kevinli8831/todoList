<template>
  <div class="d-flex pa-5 backgroundColor flex">
    <Calendar class="mr-5" />
    <div class="full-width d-flex" style="min-height: 600px; gap: 20px">
      <Todo
        :completed="completed"
        :list="todoList"
        :remain="remain"
        style="flex: 50%"
        @addTodo="addTodo"
        @deleteItem="deleteItem"
        @editItem="editItem"
        @finishItem="finishItem"
      />
      <FinishList
        :finish-list="finishList"
        style="flex: 50%"
        @FinishDeleteItem="FinishDeleteItem"
        @backToTodoList="backToTodoList"
      ></FinishList>
    </div>
  </div>
</template>

<script>
import moment from "moment";
import Calendar from "@/components/Calendar";
import Todo from "@/components/Todo";
import FinishList from "@/components/FinishList";

export default {
  name: "todoList",
  components: { FinishList, Todo, Calendar },
  data() {
    return {
      todoList: [],
      finishList: [],
    };
  },
  computed: {
    remain() {
      return this.todoList.length;
    },
    completed() {
      return this.finishList.length;
    },
  },
  methods: {
    moment,
    addTodo(text, date) {
      this.todoList.push(
        Object.assign(
          {},
          {
            text: text,
            created_at: date,
          }
        )
      );
    },
    finishItem(index) {
      console.log(index, "index");
      this.todoList[index].finished_at = moment()._d;
      this.finishList.push(this.todoList[index]);
      this.todoList.splice(index, 1);
    },
    editItem(text, index) {
      this.todoList[index].text = text;
      console.log(text, index, "index");
    },
    deleteItem(index) {
      this.todoList.splice(index, 1);
    },
    FinishDeleteItem(index) {
      this.finishList.splice(index, 1);
    },
    backToTodoList(i) {
      try {
        this.finishList[i].created_at = moment()._d;
        this.todoList.push(this.finishList[i]);
        this.finishList.splice(i, 1);
      } catch (e) {
        console.log(e);
      }
    },
  },
};
</script>

<style scoped></style>
