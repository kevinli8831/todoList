<template>
  <div class="full-height">
    <div class="d-flex justify-space-between px-5 mb-5">
      <div>
        <h2>TODO</h2>
        <span>
          <span style="color: rgba(250, 0, 0, 0.83)">
            Remaining:{{ remain }}
          </span>
          |
          <span class="mr-5" style="color: deepskyblue">
            Completed:{{ completed }}</span
          >
          <v-progress-circular :value="progress"></v-progress-circular>
        </span>
      </div>

      <div>
        <v-btn
          class="mr-2"
          color="primary"
          dark
          style="width: 100px"
          @click="isAdd = !isAdd"
        >
          <v-icon>add_circle_outline</v-icon>
        </v-btn>
        <v-btn class="mr-2" color="yellow" dark @click="handleMode('edit')">
          <v-icon>edit</v-icon>
        </v-btn>
        <v-btn class="mr-2" color="danger" dark @click="handleMode('delete')">
          <v-icon>delete</v-icon>
        </v-btn>
      </div>
    </div>
    <v-scroll-y-transition>
      <div v-if="isAdd" class="addCard mb-2">
        <h3>新增項目</h3>
        <div class="d-flex" style="gap: 10px">
          <v-text-field
            v-model="text"
            dense
            hide-details
            outlined
          ></v-text-field>
          <v-btn color="primary" @click="emitAddTodo">新增</v-btn>
        </div>
      </div>
    </v-scroll-y-transition>
    <!--    todoItem-->

    <div class="todoBackground full-height">
      <transition-group mode="out-in" name="flip-list">
        <todo-item
          v-for="(item, i) in list"
          :key="`s-${i}`"
          :created_at="item.created_at"
          :index="i"
          :mode="mode"
          :text="item.text"
          @deleteItem="deleteItem"
          @editItem="editItem"
          @finishItem="finishItem"
        ></todo-item>
      </transition-group>
    </div>
  </div>
</template>

<script>
import moment from "moment";
import TodoItem from "@/components/todoItem";

export default {
  name: "Todo",
  components: { TodoItem },
  props: {
    remain: {
      type: Number,
    },
    completed: {
      type: Number,
    },
    list: {
      type: Array,
      default: () => [{ text: "", date: "" }],
    },
  },
  data() {
    return {
      mode: "add",
      isDelete: false,
      isAdd: false,
      text: "",
      modifiedText: "",
      date: "",
    };
  },
  computed: {
    progress() {
      return (this.completed / (this.remain + this.completed)) * 100;
    },
  },
  methods: {
    moment,
    handleMode(text) {
      if (text === this.mode) {
        this.mode = "add";
      } else this.mode = text;
    },
    emitAddTodo() {
      this.date = moment()._d;
      this.$emit("addTodo", this.text, this.date);
    },
    finishItem(index) {
      this.$emit("finishItem", index);
    },
    deleteItem(index) {
      this.$emit("deleteItem", index);
    },
    editItem(text, index) {
      this.$emit("editItem", text, index);
    },
  },
};
</script>

<style scoped>
.addCard {
  box-shadow: rgb(0 0 0 / 5%) 0px 6px 24px 0px, rgb(0 0 0 / 8%) 0px 0px 0px 1px;

  border-radius: 10px;
  padding: 20px;
  background-color: #f4f9ee;
}

.todoBackground {
  padding: 10px;
  border-radius: 10px;
  background-color: #e4e4e4;
  box-shadow: rgb(0 0 0 / 5%) 0px 6px 24px 0px, rgb(0 0 0 / 8%) 0px 0px 0px 1px;
}

.list-enter-active,
.list-leave-active {
  transition: all 0.5s;
}

.list-enter, .list-leave-to /* .list-leave-active below version 2.1.8 */ {
  opacity: 0;
  transform: translateY(30px);
}
</style>