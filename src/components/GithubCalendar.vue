<template>
  <div id="github-stats">
    <svg class="cal-wrapper" :height="8 * squareSize">
      <!-- <g class="cal-months" v-for="(month, i) in ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec']" :key="month">
        <text
          fill="#000000"
          :y="1.25 * squareSize"
          :x="(i * 2 * (squareSize + 1)) + (squareSize + 1)">{{ month }}</text>
      </g> -->
      <g class="cal-week" v-for="(week, i) in values" :key="i">
        <rect class="cal-day" v-for="(day, j) in week.contributionDays" :key="j"
          :style="{fill: rangeColors[contribCount(day.contributionCount)]}"
          :width="squareSize"
          :height="squareSize"
          :x="i * (squareSize + 1)"
          :y="j * (squareSize + 1)"
        />
      </g>
      <!-- <g class="cal-legend" :y="9 * squareSize">
        <rect v-for="(color, i) in rangeColors" :key="color"
          :style="{fill: color}"
          :width="squareSize"
          :height="squareSize"
          :x="i * (squareSize + 1)"
        /> 
      </g> -->
    </svg>
  </div>
</template>

<script>
import axios from "axios";

const DEFAULT_RANGE_COLOR = ['#ebedf0', '#c6e48b', '#7bc96f', '#239a3b', '#196127']

export default {
  name: "GithubCalendar",
  props: {
    user: {
      required: true,
      type: String
    },
    months: {
      type: Number,
      default: 12
    },
    rangeColors: {
      type: Array,
      default: () => DEFAULT_RANGE_COLOR
    }
  },
  data() {
    return {
      values: [],
      squareSize: 0,
      gh_token: process.env.VUE_APP_GHTOKEN
    }
  },
  methods: {
    contribCount(count) {
      return count >= this.rangeColors.length ? this.rangeColors.length - 1 : count
    }
  },
  mounted(){
    axios
      .post(
        "https://api.github.com/graphql",
        {
          query: `{
                  user(login: "${this.user}") {
                    contributionsCollection {
                      contributionCalendar{
                        totalContributions,
                        weeks{
                          contributionDays{
                            date,
                            contributionCount
                          },
                        }
                      }
                    }
                  }
                }`
        },
        {
          headers: { Authorization: `Bearer ${this.gh_token}` }
        }
      )
      .then(res => {
        this.values = res.data.data.user.contributionsCollection.contributionCalendar.weeks.slice(53 - (this.months * 4))
        this.squareSize = document.getElementById("github-stats").offsetWidth / this.values.length - 1
      });
  }

}
</script>

<style lang="scss">
  #github-stats {
    width: 90%;
  }
  .cal-wrapper {
    width: 100%;
    // border: 1px solid black;
    
    .cal-legend {
      margin-top: 50%;
    }
    .cal-day {
      &:hover {
        stroke-width: 1;
        stroke: black;
      }
    }
  }
</style>
