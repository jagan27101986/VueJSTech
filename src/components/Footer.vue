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
position: absolute;
  bottom: 0;
  width: 100%;
  height: 2.5rem;
background: #222;
padding:6px;
display: flex;
justify-content: center;
align-items: center;

}
p {
color:lightgreen;
text-align:center;
}
</style>
