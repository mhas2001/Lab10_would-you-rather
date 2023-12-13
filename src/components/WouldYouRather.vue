<template>
  <div class="wyr">
    <h2>...Would You Rather???</h2>

    <!-- The child will take the parents props and show those values here -->
    <h1>{{ questions }}</h1>

    <!-- Radio buttons -->

    <!-- Need to v-bind value data from parent to handle data to input into radio buttons, since by default they do not have any values -->
    <!-- Wizard -->
    <input
        type="radio"
        id="choiceOne"
        v-model="choice"
        v-bind:value="choiceOne"
        v-on:change="choiceMade"
    />
    <label for="choiceOne">{{ choiceOne }}</label>

    <!-- Superhero -->
    <input
        type="radio"
        id="choiceTwo"
        v-model="choice"
        v-bind:value="choiceTwo"
        v-on:change="choiceMade"
    />
    <label for="choiceTwo">{{ choiceTwo }}</label>
  </div>
</template>

<script>
export default {
  name: 'wouldYouRather',
  props: {
    // For props in this case, we need to specify the type of prop (like variable params essentially) and not values
    // So we have 3 data that we want to send here, the wyr_question, and those 2 choices from the question
    questions: String,
    choiceOne: String,
    choiceTwo: String,
  },

  data() {
    return {
      choice: '',
    };
  },

  methods: {
    choiceMade() {
      // Give answer back to parent by using this vue method
      // $emit needs an event name and also along with data as part of the message to send back what happen with the data given to parent
      this.$emit('answer-changed', this.choice);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 45px 0 0;
}

h2 {
  padding-left: 20px;
  text-align: left;
  font-size: 25px;
}
.wyr {
  border: 3px black solid;
  /* background-color: #42b983; */
  background-image: linear-gradient(to bottom, #42b983, #ffffff);
  margin: 10px;
}
label {
  font-size: 20px;
  font-weight: bold;
}
</style>
