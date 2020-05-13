<template>
<header>
<h1> {{title}}</h1>
</header>
</template>

<script>
export default {
  name: 'Header',
  data() {
    return {
    title: 'Next to go'
    }
  }
}
</script>

<style scoped>
header {
background: green;
padding:10px;
margin-bottom:20px;
}
h1 {
color:#222;
text-align:center;
}
</style>
