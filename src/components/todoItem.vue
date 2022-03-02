<template>
  <div>
    <div class="d-flex justify-space-between todoItem">
      <div v-if="!isEdit">{{ text }}</div>
      <input
        v-else
        id="modifiedText"
        v-model="modifiedText"
        style="border: 1px solid black; border-radius: 5px"
        type="text"
      />
      <div>
        <v-btn v-if="mode === `add`" color="info" x-small @click="finishItem()"
          >完成
        </v-btn>
        <v-btn
          v-if="mode === `edit`"
          color="yellow"
          x-small
          @click="editItem(modifiedText)"
          >修改
        </v-btn>
        <v-btn
          v-if="mode === `delete`"
          color="danger"
          x-small
          @click="deleteItem()"
          >刪除
        </v-btn>
      </div>
    </div>
    <div class="text-right" style="font-size: 10px">
      <v-icon>alarm</v-icon>
      {{ moment(created_at).format("YYYY-MM-DD HH:mm") }}
    </div>
  </div>
</template>

<script>
import moment from "moment";

export default {
  name: "todoItem",
  props: {
    text: {
      type: String,
      default: "",
    },
    index: {
      type: Number,
      default: 0,
    },
    created_at: {
      type: Date,
      default: null,
    },
    mode: {
      type: String,
      default: "add",
    },
  },
  computed: {
    computedText: {
      set(v) {
        this.modifiedText = v;
      },
      get() {
        return this.text;
      },
    },
  },
  data() {
    return {
      isEdit: false,
      modifiedText: "",
    };
  },
  methods: {
    moment,
    finishItem() {
      this.$emit("finishItem", this.index);
    },
    deleteItem() {
      this.$emit("deleteItem", this.index);
    },
    editItem(text) {
      this.isEdit = !this.isEdit;
      this.$emit("editItem", text, this.index);
    },
  },
};
</script>

<style scoped>
.todoItem {
  min-height: 30px;
  padding: 0px 10px;
  display: flex;
  align-items: center;
  border-radius: 5px;
  background-color: white;
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
