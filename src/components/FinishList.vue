<template>
  <div>
    <div class="d-flex justify-space-between px-5 mb-5">
      <h2>Done</h2>
      <div>
        <v-btn color="danger">
          <v-icon>delete</v-icon>
        </v-btn>
      </div>
    </div>
    <div class="todoBackground full-height">
      <template v-for="(item, i) in finishList">
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
  name: "FinishList",
  props: {
    finishList: {
      type: Array,
      default: () => [{ text: "", date: "" }],
    },
  },
};
</script>

<style scoped>
.todoBackground {
  padding: 10px;
  border-radius: 10px;
  background-color: #e4e4e4;
  box-shadow: rgb(0 0 0 / 5%) 0px 6px 24px 0px, rgb(0 0 0 / 8%) 0px 0px 0px 1px;
}
</style>
