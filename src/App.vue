<template>
  <div id="app">
    <h1>{{ msg }}</h1>
    <div>
      <label>Find mentor by skill:</label>
      <input type="text" v-model="search" placeholder="Search for skill.."/>
    </div>
    <div class="wrapper">
      <div class="card" v-for="mentor in filteredList">
        <a v-bind:href="mentor.link" target="_blank">
          <img v-bind:src="mentor.img" height="300px" width="300px"/><br/>
        </a>
        <small>mentor: {{ mentor.name }}</small><br/>
        <small>BU: {{ mentor.bu }}</small>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

class Mentor {
  constructor(name, businessUnit, link, img, skills) {
    this.name = name;
    this.bu = businessUnit;
    this.link = link;
    this.img = img;
    this.skills = skills
  }
}
export default {
  name: 'app',
  data () {
    return {
      msg: 'Welcome Mentors and Mentees!',
      search: '',
      mentorList : [
        new Mentor(
          'Vue.js',
          'TES',
          'Chris',
          require('./assets/robot3.png'),
          ['kanban', 'scrum']
        ),
        new Mentor(
          'React.js',
          'Sales',
          'Tim',
          require('./assets/robot4.jpg'),
          ['mentoring', 'planning', 'people management']
        ),
        new Mentor(
          'Angular.js',
          'Marketing',
          'Sam',
          require('./assets/robot3.png'),
          ['kanban', 'scrum', 'mentoring', 'planning', 'people management', 'c#']
        ),
        new Mentor(
          'Ember.js',
          'Engine Room',
          'Rachel',
          require('./assets/robot4.jpg'),
          ['people management','tech lead', 'python', 'java', 'javascript']
        ),
        new Mentor(
          'Meteor.js',
          'Quality Engineering',
          'Chris',
          require('./assets/robot3.png'),
          ['kanban', 'people management','tech lead', 'ruby', 'c#']
        ),
        new Mentor(
          'Aurelia',
          'Boss',
          'Tim',
          require('./assets/robot4.jpg'),
          ['kanban', 'scrum', 'mentoring','python', 'java', 'javascript', 'ruby']
        )
      ]
    }
  },
  computed: {
    filteredList() {
      return this.mentorList.filter(mentor => {
        if (this.search === '') return mentor;
        return mentor.skills.includes(this.search.toLowerCase());
      });
    }
  },
  // #TODO: once an api is made to return data, use this service
  // created() {
  //   axios
  //     .get(`http://jsonplaceholder.typicode.com/posts`)
  //     .then(response => {
  //       this.mentorList = response.data.mentors
  //     })
  //     .catch(e => {
  //       this.errors.push(e)
  //     })
  // }
}
</script>

<style >
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

.wrapper {
  display: flex;
  max-width: 100%;
  flex-wrap: wrap;
  padding-top: 12px;
}

.card {
  box-shadow: rgba(0, 0, 0, 0.117647) 0px 1px 6px, rgba(0, 0, 0, 0.117647) 0px 1px 4px;
  max-width: 100%;
  margin: 12px;
  transition: .15s all ease-in-out;
  &:hover {
    transform: scale(1.1);
  }
  a {
    text-decoration: none;
    padding: 12px;
    color: #03A9F4;
    font-size: 24px;
    display: flex;
    flex-direction: column;
    align-items: center;
    img {
      height: 100px;
    }
    small {
      font-size: 10px;
      padding: 4px;
    }
  }
}
</style>
