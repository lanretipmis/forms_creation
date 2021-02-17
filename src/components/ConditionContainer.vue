<template>
<div  class="formsContainer">
  <SelectInput
                @updateCondition="updateCondition"
                v-bind:isConditionInput="true"
               v-bind:label="label" v-bind:placeholder="placeholder"
               v-bind:options="options" :key="placeholder"/>
  <SelectInput
    v-if="typeOfSub === 'select'"
    v-bind:label="subLabel"
    v-bind:placeholder="subPlaceholder" v-bind:options="subOptions" :key="nameOfSub"/>
</div>
</template>

<script>
import SelectInput from '@/components/SelectInput.vue';

export default {
  name: 'ConditionContainer',
  components: {
    SelectInput,
  },
  props: {
    label: String,
    placeholder: String,
  },
  data() {
    return {
      options: [
        { text: 'Возраст респондента', value: 'Возраст респондента' },
        { text: 'Тип карты лояльности', value: 'Тип карты лояльности' },
        { text: 'Статус карты лояльности', value: 'Статус карты лояльности' },
      ],
      nameOfSub: this.placeholder,
      typeOfSub: '',
      subLabel: '',
      subPlaceholder: '',
      subOptions: [],
      componentKey: 0,
      dataForServer: {
        condition: this.nameOfSub,
        answer: '',
      },
    };
  },
  methods: {
    getSubInput() {
      switch (this.nameOfSub) {
        case 'Возраст респондента':
          this.options[0].selected = true;
          this.typeOfSub = 'range';
          this.componentKey += 1;
          break;
        case 'Тип карты лояльности':
          this.options[1].selected = true;
          this.subLabel = 'Тип карты';
          this.typeOfSub = 'select';
          this.subOptions = [
            { text: 'Gold', value: 'Gold' },
            { text: 'Silver', value: 'Gold' },
            { text: 'Bronze', value: 'Gold' },
          ];
          this.componentKey += 1;
          break;
        case 'Статус карты лояльности':
          this.options[2].selected = true;
          this.subLabel = 'Статус';
          this.typeOfSub = 'select';
          this.subOptions = [
            { text: 'Активна', value: 'Активна' },
            { text: 'Заморожена', value: 'Заморожена' },
            { text: 'Оформляется', value: 'Оформляется' },
          ];
          this.componentKey += 1;
          break;
        default:
          break;
      }
    },
    updateCondition(options) {
      this.options = options;
      const index = options.findIndex((option) => (option.selected ? option.text : ''));
      this.nameOfSub = options[index].text;
      this.getSubInput();
    },
  },
  mounted() {
    this.getSubInput();
    console.log(this.options);
  },
};
</script>

<style scoped>
.formsContainer{
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  justify-content: center;
  padding: 15px;
  background: sandybrown;
  max-width: 350px;
  border-radius: 7px;
  margin: 10px;
}
</style>
