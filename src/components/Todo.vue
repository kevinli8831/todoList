<template>
  <div class="full-height">
    <div class="d-flex justify-space-between px-5 mb-5">
      <h2>TODO</h2>
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
        <v-btn class="mr-2" color="yellow" dark>
          <v-icon>edit</v-icon>
        </v-btn>
        <v-btn class="mr-2" color="danger" dark>
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
          <v-btn color="primary" @click="submitData">新增</v-btn>
        </div>
      </div>
    </v-scroll-y-transition>
    <!--    todoItem-->

    <div class="todoBackground full-height">
      <template v-for="(item, i) in list">
        <div :key="`s-${i}`" class="d-flex justify-space-between todoItem">
          <div>{{ item.text }}</div>
          <div>
            <v-btn text>加入完成事項</v-btn>
          </div>
        </div>
      </template>
    </div>
  </div>
</template>

<script>
export default {
  name: "Todo",
  props: {
    list: {
      type: Array,
      default: () => [{ text: "", date: "" }],
    },
  },
  data() {
    return { isAdd: false, text: "", date: "" };
  },
  methods: {
    submitData() {
      this.$emit("addTodo", this.text);
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

.todoItem {
  padding: 0px 10px;
  display: flex;
  align-items: center;
  border-radius: 5px;
  background-color: white;
  box-shadow: rgb(0 0 0 / 5%) 0px 6px 24px 0px, rgb(0 0 0 / 8%) 0px 0px 0px 1px;
}

.todoBackground {
  padding: 10px;
  border-radius: 10px;
  background-color: #e4e4e4;
  box-shadow: rgb(0 0 0 / 5%) 0px 6px 24px 0px, rgb(0 0 0 / 8%) 0px 0px 0px 1px;
}
</style>
