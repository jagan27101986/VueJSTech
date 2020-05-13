<template>
<footer>
<p> {{title}}</p>
</footer>
</template>

<script>
export default {
  name: 'Footer',
  data() {
    return {
    title: 'Copyright 2020'
    }
  }
}
</script>

<style scoped>
footer {
background: #222;
padding:6px;

}
p {
color:lightgreen;
text-align:center;
}
</style>
