<template>
  <div  v-bind:class="!isConditionInput ? 'subInput' : ''">
    <p>{{ label }}</p>
    <select @change.prevent="changeCondition">
<!--      <span>{{ placeholder }}</span>-->
      <option v-for="option in options" :key="option.value"
               v-bind:value="options.findIndex(opt => opt.text === option.text)"
               v-bind:selected="!!option.selected">
        {{ option.text }}
      </option>
    </select>

  </div>
</template>

<script>
export default {
  name: 'SelectInput',
  props: {
    label: String,
    placeholder: String,
    options: Array,
    isConditionInput: Boolean,
  },
  methods: {
    changeCondition(event) {
      if (this.isConditionInput) {
        const { options } = this;
        const index = options.findIndex((option) => option.selected);
        delete options[index].selected;
        options[event.target.value].selected = true;
        this.$emit('updateCondition', options);
      }
    },
  },
};
</script>

<style scoped>
div{
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 100%;
}
p{
  font-size: 20px;
  margin-right: 15px;
}
select{
  width: 200px;
  border-radius: 7px;
  background: beige;
}
.subInput {
}
</style>
