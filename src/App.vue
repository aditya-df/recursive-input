<template>
  <div class="flex flex-col justify-center items-center min-h-screen space-y-3">
    <div class="flex justify-between w-64">
      <p>test</p>
      <button class="border rounded px-2" @click="add(items)">
        + Sub Item
      </button>
    </div>
    <div>
      <div v-for="(item, i) in items" :key="item.id" class="space-y-2">
        <nested-input-item
          :parentItem="item"
          :index="i"
          v-model:modelValue="item.name"
          @removeItem="remove(item)"
        ></nested-input-item>
      </div>
    </div>
  </div>
</template>

<script>
import NestedInputItem from "./components/NestedInputItem.vue";
export default {
  components: { NestedInputItem },
  data() {
    return {
      items: [
        {
          id: "1",
          name: "",
          subItems: [],
        },
      ],
    };
  },
  methods: {
    remove(item) {
      this.items = this.items.filter((element) => {
        return element.id !== item.id;
      });
    },
    add(parentItem) {
      let id = parentItem.length
        ? +parentItem.at(-1).id + 1
        : 1;
      parentItem.push({
        id: `${id}`,
        name: "",
        subItems: [],
      });
    },
  },
};
</script>
