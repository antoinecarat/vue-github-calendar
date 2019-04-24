<template>
  <div id="app">
    <h1>Github Calendar Demo</h1>
    <!-- <div class="calendar-form">
      <label for="username">Username:</label>
      <input name="username" type="text" v-model="username">
      <label for="months">Months from now:</label>
      <input type="number" v-model.number="months">
      <label for="size">Size:</label>
      <select name="size" id="" v-model="size">
        <option value="full">Full</option>
        <option value="half">Half</option>
        <option value="third">Third</option>
        <option value="quarter">Quarter</option>
      </select>
    </div> -->
    <div :class="{ full: size == 'full', half: size == 'half', third: size == 'third', quarter: size == 'quarter', }">
      <GithubCalendar :user="username" :months="months" />
    </div>
  </div>
</template>

<script>
// import GithubCalendar from "@acarat/vue-github-calendar";
import GithubCalendar from "./components/GithubCalendar.vue"

export default {
  name: "app",
  components: {
    GithubCalendar
  },
  data: function() {
    return {
      username: "antoinecarat",
      months: 12,
      size: "full"
    };
  }
};
</script>

<style lang="scss">
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;

  display: flex;
  flex-flow: column nowrap;
  justify-content: flex-start;
  align-items: flex-start;
  padding: 2%;
  width: 100%;

  .calendar-form {
    display: flex;
    flex-flow: row nowrap;
    justify-content: flex-start;
    align-items: flex-start;
    margin-bottom: 2rem;

    label {
      &:first-child {
        margin-left: 0;
      }
      margin-left: 1rem;
      margin-right: .5rem;
    }
  }

  .full {
    width: 100%;
  }

  .half {
    width: 50%;
  }

  .third {
    width: 33%;
  }

  .quarter {
    width: 25%;
  }

}
</style>
