<template>
  <div id="app">
    <div class="box-content">
      <div class="app-header">
        <Header></Header>
      </div>
      <div class="app-content">
        <Content></Content>
      </div>
      <div class="app-footer">
        <Footer></Footer>
      </div>
    </div>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Footer from "./components/Footer.vue";
import Content from "./components/Content.vue";

export default {
  name: "App",
  components: {
    Header,
    Footer,
    Content,
  },
};
</script>

<style lang='less' scoped>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
#app {
  margin: 0 auto;
  background-image: linear-gradient(#e66465, #9198e5);
  width: 600px;
  .app-header {
  }

  .app-content {
    content {
    }
  }

  .app-footer {
    footer {
    }
  }
}
</style>
