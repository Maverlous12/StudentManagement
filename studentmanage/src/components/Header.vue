<template>
  <Header class="header">
    <div class="header__nav">{{ title }}</div>
  </Header>
</template>

<script>
export default {
  name: 'compt-header',
  props: {
    title: String,
  },
};
</script>

<style>
.header {
  font-size: 30px;
  font-weight: 600;
}
</style>
