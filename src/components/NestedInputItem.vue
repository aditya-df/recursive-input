<template>
  <div class="space-y-2">
    <input-item
      :item="parentItem"
      :index="index"
      @addSubItem="add(parentItem)"
      @removeItem="$emit('removeItem', parentItem)"
      v-model:modelValue="parentItem.name"
    ></input-item>

    <div class="ml-4" v-if="parentItem.subItems">
      <nested-input-item
        v-for="(item,i) in parentItem.subItems"
        :key="item.id"
        :parentItem="item"
        :index="i"
        v-model:modelValue="item.name"
        @removeItem="remove(item)"
      ></nested-input-item>
    </div>
  </div>
</template>

<script>
import InputItem from "../components/InputItem.vue";
export default {
  components: { InputItem },
  props: {
    parentItem: {
      required: true,
      type: Object,
    },
    index:{
        type:Number
    }
  },
  methods: {
    add(parentItem) {
      parentItem.subItems.unshift({
        id: `${parentItem.id}.${parentItem.subItems.length+1}`,
        name: "",
        subItems: [],
      });
    },
    remove(item) {
      this.parentItem.subItems = this.parentItem.subItems.filter((element) => {
        return element.id !== item.id;
      });
    },
  },
};
</script>
