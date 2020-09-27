<template>
  <transition-group name="fade" tag="div" @beforeEnter="beforeEnter" @enter="enter" @leave="leave">
    <div
      class="row d-flex mb-3 align-items-center"
      v-for="(item, index) in data.results"
      :key="item.title"
      :data-index="index"
    >
      <div class="col-4">
        <img class="img-fluid d-block" :src="item.thumbnail" :alt="item.title">
      </div>
      <div class="col">
        <h3 class="text-info">{{ item.title }}</h3>
        <p class="mb-0">{{ item.ingredients }}</p>
      </div>
    </div>
  </transition-group>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      data: {}
    }
  },
  beforeMount(){
    this.getName();
  },
  methods: {
    async getName(){
      const proxyurl = "https://cors-anywhere.herokuapp.com/";
      const url = "http://www.recipepuppy.com/api/";
      const res = await fetch(proxyurl + url);
      const data = await res.json();
      this.data = data;
    }
  }
};
</script>