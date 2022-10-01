<template>
  <header>
    <div class="d-flex align-items-center" v-b-toggle.sidebar-backdrop>
      <button class="btn btn-primary">Menu</button>
    </div>
    <b-sidebar id="sidebar-backdrop" :backdrop-variant="variant" backdrop shadow class="">
      <h2 class="mb-2 ml-3">Menu</h2>
      <ul>
        <li>
          <nuxt-link to="/">Home</nuxt-link>
        </li>
        <li>
          <nuxt-link to="/profile/123456/">Profile</nuxt-link>
        </li>
        <li>
          <nuxt-link to="/profile/123456/edit">Profile Edit</nuxt-link>
        </li>
      </ul>
    </b-sidebar>
  </header>
</template>

<script>
export default {
name: 'Menu'
}
</script>

<style>

</style>