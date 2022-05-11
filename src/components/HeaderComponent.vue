<template>
  <div class="header">
      <h1 class='link'>Notifications</h1>
  </div>
</template>

<script>
export default {
  name: 'HeaderComponent',

}
</script>

<style scoped>

.header {
  margin-top: 5px;
  border-radius: 4px;
  overflow: hidden;
  background-color: #333;
  position: fixed;
  top: 0;
  width: 100%
}

.header .link {
  /* float: left; */
  color: #f2f2f2;
  padding: 14px 16px;
  text-decoration: none;
  font-size: 17px;
}
</style>
