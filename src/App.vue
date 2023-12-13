<template>
  <div id="app">
    <!-- Title -->
    <h1>Would You Rather︖⸮¿</h1>
    <h1>Would You Rather︖⸮¿</h1>
    <h1>Would You Rather︖⸮¿</h1>
    <h1>Would You Rather︖⸮¿</h1>
    <h2>Please make your choice!</h2>

    <!-- Include data from other files must be sent to the main app.vue -->
    <!-- So in this case, If we need the file, "would you rather" data, props, methods or whatever its in that file, we import that component here to share, and that component is essentially our "files" to render to this main app. I think for props, we need to send that prop argument here but need to set those props handling in the child component as the child prop needs to expect to receive data  -->

    <!-- Use v-bind to bind those prop param and the prop value from app here -->
    <!-- Event names uses dashes and while function names uses camel cases -->
    <!-- answer-changed is the event that the parent is listening from the child component, and so the parent is able to handle that event with a function call, in this case, display a message too users their choice -->
    <!-- v-bind:questions="wyrQuestion"
      v-bind:answer1="wyrAnswer1"
      v-bind:answer2="wyrAnswer2"
      v-on:answer-changed="answerChange" -->
    <Would-You-Rather
        v-for="question of questionsToAskUsers"
        v-bind:questions="question.wyrQuestion"
        v-bind:choiceOne="question.wyrAnswer1"
        v-bind:choiceTwo="question.wyrAnswer2"
        v-on:answer-changed="answerChange(question.id, $event)"
    ></Would-You-Rather>

    <!-- Users choices list  -->
    <div class="usersChoicePickedList">
      <ul v-show="usersChoices.length > 0">
        <li
            v-for="choice of usersChoices"
            v-bind:key="choice.userSelectionMessage"
        >
          {{ choice.userSelectionMessage }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import WouldYouRather from './components/WouldYouRather.vue';

export default {
  name: 'App',
  components: {
    WouldYouRather,
  },
  data() {
    return {
      questionsToAskUsers: [
        {
          id: 0,
          wyrQuestion: 'Be a wizard or a superhero?',
          wyrAnswer1: 'Wizard',
          wyrAnswer2: 'Superhero',
        },
        {
          id: 1,
          wyrQuestion:
              'Start a colony on another planet or be the leader of a small country on Earth?',
          wyrAnswer1: 'Start a colony on another planet',
          wyrAnswer2: 'Be the leader of a small country on Earth',
        },
        {
          id: 2,
          wyrQuestion:
              'Have a magic freezer that always has all your favorite ice cream flavors or one that has a different ice cream flavor every time you open the door?',
          wyrAnswer1: 'Favorite ice cream flavors',
          wyrAnswer2: 'Different ice cream flavor every time you open the door',
        },
        {
          id: 3,
          wyrQuestion:
              'Would you rather live in a base under the ocean or a floating base in the sky?',
          wyrAnswer1: 'Live in a base under the ocean',
          wyrAnswer2: 'Live in a floating base in the sky',
        },
      ],

      usersChoices: [],
    };
  },

  methods: {
    // The function answerChanged handles the emitted data from child component here.
    // Since the parameter, 'choice' is being passed through, answerChange has access to emitted data sent from the child component, so 'choice' in this case (connected to wyr component) have access to the argument data, which is the users pick.

    // Add or modify existing users choice based on question id
    answerChange(questionId, choice) {
      let currentChoice = this.usersChoices.findIndex(function (userChoice) {
        return userChoice.questionId === questionId;
      });
      if (currentChoice !== -1) {
        this.usersChoices[
            currentChoice
            ].userSelectionMessage = `Wow! you choose ${choice}`;
      } else {
        this.usersChoices.push({
          questionId,
          userSelectionMessage: `Wow! you choose ${choice}`,
        });
      }
    },
  },
};
</script>

<style>
body {
  background: darksalmon;
}

.usersChoicePickedList {
  border: 1rem solid royalblue;
  padding: 10px;
}
ul {
  list-style: square;
  text-transform: uppercase;
  font-size: 20px;
  font-weight: bold;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  background: lightblue;
  padding-top: 1px;
}
</style>
