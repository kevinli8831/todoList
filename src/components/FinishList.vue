<template>
  <div>
    <div class="d-flex justify-space-between px-5 mb-5">
      <h2>Done</h2>
      <div>
        <v-btn color="danger" dark @click="isDelete = !isDelete">
          <v-icon>delete</v-icon>
        </v-btn>
      </div>
    </div>
    <div class="todoBackground full-height">
      <transition-group name="list">
        <div v-for="(item, i) in finishList" :key="`s-${i}`">
          <div class="d-flex justify-space-between todoItem">
            <div>{{ item.text }}</div>
            <div>
              <v-btn
                v-if="isDelete"
                color="danger"
                x-small
                @click.stop="FinishDeleteItem"
                >刪除
              </v-btn>
              <v-btn
                v-else
                color="danger"
                x-small
                @click.stop="backToTodoList(i)"
                >撇回
              </v-btn>
            </div>
          </div>
          <div class="text-right" style="font-size: 10px">
            <v-icon>alarm</v-icon>
            {{ moment(item.finished_at).format("YYYY-MM-DD HH:mm") }}
          </div>
        </div>
      </transition-group>
    </div>
  </div>
</template>

<script>
import moment from "moment";
export default {
  name: "FinishList",
  props: {
    finishList: {
      type: Array,
      default: () => [{ text: "", date: "" }],
    },
  },
  data() {
    return {
      isDelete: false,
    };
  },
  methods: {
    moment,

    FinishDeleteItem(i) {
      this.$emit("FinishDeleteItem", i);
    },
    backToTodoList(i) {
      this.$emit("backToTodoList", i);
    },
  },
};
</script>

<style scoped>
.list-enter-active,
.list-leave-active {
  transition: all 0.5s;
}

.list-enter, .list-leave-to /* .list-leave-active below version 2.1.8 */ {
  opacity: 0;
  transform: translateY(30px);
}

.todoBackground {
  padding: 10px;
  border-radius: 10px;
  background-color: #e4e4e4;
  box-shadow: rgb(0 0 0 / 5%) 0px 6px 24px 0px, rgb(0 0 0 / 8%) 0px 0px 0px 1px;
}

.todoItem {
  min-height: 30px;
  padding: 0px 10px;
  display: flex;
  align-items: center;
  border-radius: 5px;
  background-color: white;
  box-shadow: rgb(0 0 0 / 5%) 0px 6px 24px 0px, rgb(0 0 0 / 8%) 0px 0px 0px 1px;
}
</style>