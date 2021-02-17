<template>
  <button @click="addCondition">Добавить Условие</button>
  <ConditionContainer
    v-for="condition in conditions" :key="condition.value"
    v-bind:label="condition.label"
    v-bind:placeholder="condition.placeholder">
    {{condition}}
  </ConditionContainer>

</template>

<script>
import ConditionContainer from './components/ConditionContainer.vue';

export default {
  name: 'App',
  components: {
    ConditionContainer,
  },
  data() {
    return {
      conditions: [
        // { label: 'Условие', placeholder: 'Статус карты лояльности', value: 1 },
      ],
      dateFromAllConditions: [
        {
          condition: 'Cnenfec',
          answer: 'asd',
        },
      ],
    };
  },
  methods: {
    addCondition() {
      this.conditions.push({
        label: `Условие ${this.conditions.length + 1}`,
        placeholder: 'Статус карты лояльности',
        value: this.conditions.length,
      });
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}
button{
  background: #42b983;
  font-size: 20px;
  padding: 10px 15px;
  border: none;
  border-radius: 7px;
}
</style>
