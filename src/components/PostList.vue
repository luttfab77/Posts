<template>
  <div v-if="error">
    <h2>Error: {{ error }}</h2>
  </div>
  <div v-if="loading">
    <h2>Loading data...</h2>
  </div>
  <h2>Posts</h2>
  <span><b>UserID<b></span><span><b>ID</b></span><span><b>Title</b></span><span><b>Body</b></span>
  <ul>
    <li v-for="item, index in data" :key="item.id" :index="index">
      <span v-if="index > 0 && data[index].userId != data[index - 1].userId"> {{ item.userId }}</span>
      <span v-else-if="index == 0"> {{ item.userId }} </span>
      <span v-else> </span>
      <span> {{ item.id }}</span> 
      <span> {{ item.title }}</span> 
      <span> {{ item.body }}</span> 
    </li>
  </ul>
</template>

<script>
import { useFetch } from '../composables/UseFetch.js';

export default {
  setup() {
    const { data, error, loading } = useFetch(
      'https://jsonplaceholder.typicode.com/posts',
      {}
    );

    return {
      data,
      error,
      loading,
    };
  },
};
</script>

<style scoped>
span {
  display: inline-block;
  width: 200px;
}
ul {
  list-style-type: none;
}
</style>
