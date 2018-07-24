<template>
  <div class="test">
    <h1>users</h1>
    <form v-on:submit="addUser">
      <input type="text" v-model="newUser.name" placeholder="Enter Name">
      <br />
      <input type="text" v-model="newUser.email" placeholder="Enter Email">
      <br />
      <input type="submit" value="submit">
    </form>
    <ul>
      <li v-for="message in messages">
        {{message.tags.Title}}: {{message.name}}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'users',
  data() {
    return {
      newUser: {},
      messages: {},
    }
  },
  methods: {
    addUser: function (e) {
      console.log('Added new user');
      this.users.push({
        name: this.newUser.name,
        email: this.newUser.email,
      })
      e.preventDefault();
    },
    deletUser: function (index) {
      this.users.splice(this.users.indexOf(index), 1);
    }
  },
  created: function() {
    console.log('created Run');
    this.$http.get('https://api.synduit4.com/v1/campaign-texts', {
            headers: {
              'Content-type': 'application/json',
              'Accept': 'application/json',
              'Authorization': ''
            }
          }).then(response => {
            this.messages = response.data.data;
            console.log(response.data.data);
          })
  }
}
</script>

<style scoped>
  .contacted {
    text-decoration: line-through;
  }
</style>
