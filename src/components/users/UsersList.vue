<template>
  <button @click="confirmInput">confirm</button>
  <button @click="saveChanges">Save changes</button>
  <ul>
    <user-item
      v-for="user in users"
      :key="user.id"
      :name="user.fullName"
      :role="user.role"
    ></user-item>
  </ul>
</template>

<script>
import UserItem from './UserItem.vue';

export default {
  data() {
    return {
      changesSaved: false
    };
  },
  components: {
    UserItem
  },
  inject: ['users'],
  methods: {
    confirmInput() {
      this.$router.push('/teams');
    },
    saveChanges() {
      this.changesSaved = true;
    }
  },
  beforeRouteLeave(to, from, next) {
    console.log(' UsersList Cmp beforRouteLeave');
    console.log(to, from);
    if (this.changesSaved) {
      next();
    } else {
      const userWantsToLeave = confirm('Are you sure ?');
      next(userWantsToLeave);
    }
  }

  // beforRouteEnter(to, from, next) {
  //   console.log(to, from)
  //   next()
  // }
};
</script>

<style scoped>
ul {
  list-style: none;
  margin: 2rem auto;
  max-width: 20rem;
  padding: 0;
}
</style>
