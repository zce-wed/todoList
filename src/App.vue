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
    <div class="texiao">
      <texiao></texiao>
    </div>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Footer from "./components/Footer.vue";
import Content from "./components/Content.vue";
import texiao from "./components/texiao.vue"

export default {
  name: "App",
  components: {
    Header,
    Footer,
    Content,
    texiao
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
  box-shadow: 5px 7px 30px #9696a0;
    border-radius: 20px;
    position: absolute;
    z-index: 99;
    left: 50vw;
    left: 25vw;
    top: 50vh;
    transform: translateY(-50%);
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
  .texiao{
    background-color: tomato;
    position: absolute;

  }
}
</style>





