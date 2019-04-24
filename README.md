# vue-github-calendar
A responsive and customizable Github heatmap calendar for Vue.js

## Usage

### Install

```bash
npm install vue-github-calendar
```

### Import the component

```js
import { GithubCalendar } from "vue-github-calendar";
```

### Use the component in your Vue project

```html
  <GithubCalendar
    :user="username"
    :months="months"
    :rangeColors=['#ebedf0', '#dae2ef', '#c0ddf9', '#73b3f3', '#3886e1', '#17459e']/>
```

## Props

### username
type: String
The Github username you want to show latest activity.

### months?
type: Number
The number of months _from now_ you want to display.
_By default, you'll have the 12 past months._

### rangeColors?
type: Array
The colors used to display the amount of activity on a given day. Use this to accord the calendar with your website visual identity.
_By default, the original colors from githug will be used_

## Github token

You'll need to set an environment variable named `VUE_APP_GH_TOKEN` to be able to retrieve the data.
Use a `.env.local` file to store it or add it directly in your system's environment variables.

_Follow (this)[https://developer.github.com/v4/guides/forming-calls/#authenticating-with-graphql] to get your token._

## Incoming features

- [ ] Color range legend
- [ ] Display the week days on the left
- [ ] Display the months above the calendar
- [ ] Add tooltips (X contributions on DD-MM-YYYY)
- [ ] Allow to get a specific period (from, to)