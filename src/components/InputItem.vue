<template>
  <div class="flex space-x-2">
    <label
      for="text"
      class="block rounded-full p-2 min-w-[2rem] text-center bg-slate-400 text-white"
    >
      {{ id }}
    </label>
    <input
      type="text"
      name="text"
      id="text"
      class="border border-black rounded px-2 py-1 placeholder:text-sm"
      :class="[{ 'bg-red-100 border-red-600': item.name == '' }]"
      :value="item.name"
      @input="$emit('update:modelValue', $event.target.value)"
      placeholder="Masukkan deskripsi"
    />
    <button class="bg-red-400 rounded px-2" @click="$emit('removeItem', item)">
      remove
    </button>
    <button class="border rounded px-2" @click="$emit('addSubItem', item)">
      + Sub Item
    </button>
  </div>
</template>

<script>
export default {
  props: {
    item: {
      type: Object,
      required: true,
    },
    index: {
      type: Number,
    },
  },
  emits: ["update:modelValue", "addSubItem", "removeItem"],
  computed: {
    id() {
      if (this.item.id.includes(".")) {
        return this.item.id.split(".")[0] + "." + (this.index + 1);
      } else {
        return this.item.id;
      }
    },
  },
};
</script>
