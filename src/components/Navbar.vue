<template>
<nav v-if="user">
  <div>
    <p>Hey there {{ user.displayName }}</p>
    <p class="email">Currently logged as {{ user.email }}</p>
  </div>
  <button @click="handleClick">Logout</button>
</nav>
</template>

<script>
import userLogout from '../composables/userLogout'
import getUser from '../composables/getUser'

export default {
  setup() {
    const {error, logout} = userLogout()
    const { user } = getUser()

    console.log(user.value)

    const handleClick = async () => {
      await logout()
      if (!error.value) {
        console.log('User logged out')
      }
    }

    return { handleClick, user }
  }
}
</script>

<style>
  nav {
    padding: 20px;
    border-bottom: 1px solid #eee;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  nav p {
    margin: 2px auto;
    font-size: 16px;
    color: #444;
  }
  nav p.email {
    font-size: 14px;
    color: #999;
  }
</style>