<template>
  <div class="d-flex pa-5 backgroundColor flex">
    <Calendar class="mr-5" />
    <div class="full-width d-flex" style="min-height: 600px; gap: 20px">
      <Todo :list="todoList" style="flex: 50%" />
      <FinishList style="flex: 50%"></FinishList>
    </div>
  </div>
</template>

<script>
import Calendar from "@/components/Calendar";
import Todo from "@/components/Todo";
import FinishList from "@/components/FinishList";

export default {
  name: "todoList",
  components: { FinishList, Todo, Calendar },
  data() {
    return {
      isEdit: false,
      isDelete: false,
      isAdd: false,
      todoList: [],
      finishList: [],
    };
  },
};
</script>

<style scoped></style>