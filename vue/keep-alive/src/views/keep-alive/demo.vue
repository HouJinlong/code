<template>
  <div class="body flex justify-sb">
    <!-- app -->
    <div class="app">
      <b style="color:#776e65;line-height: 60px;">app</b>
      <div class="keep-alive">
        <b style="color:#776e65;">keep-alive</b>
        <div class="router-view">router-view</div>
      </div>
      <div class="router-view"
           style="margin: 15px;">router-view</div>
    </div>
    <!-- if -->
    <div class="app keepAlive">
      <b style="color:#776e65;line-height: 60px;">是否keepAlive</b>
      <pre v-highlight
           class="flex">
            <code>$route.meta.keepAlive</code>
        </pre>
    </div>
    <!-- routers -->
    <div class="flex flow-col align-stretch">
      <div class="router-item"
           v-for="router in routers">
        <span style="line-height: 3;">{{router.name}}</span>
        <pre v-highlight
             class="flex">
            <code v-html="router"></code>
        </pre>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data: () => ({
    routers: [
      {
        name: "index",
        meta: {
          deepth: 0.5
        }
      },
      {
        name: "list",
        meta: {
          deepth: 1,
          keepAlive: true // 需要被缓存
        }
      },
      {
        name: "detail",
        meta: {
          deepth: 2
        }
      }
    ]
  })
};
</script>

<style scoped>
.body {
  padding: 15px;
  background: #faf8ef;
  color: #776e65;
  background: url(amam.png);
}
.app {
  box-sizing: border-box;
  padding: 0 15px 15px;
  width: 300px;
  background: #eee4da;
  border: 0.5px solid #bbada0;
}
.app.keepAlive {
  width: auto;
}
.keep-alive {
  padding: 15px;
  background: #cdc1b4;
  border: 0.5px solid #bbada0;
}
.router-view {
  margin: 15px 0;
  height: 60px;
  background: #f59563;
  border: 0.5px dashed #fff;
  line-height: 60px;
  color: #fff;
  text-align: center;
}
.router-item {
  margin-bottom: 15px;
  padding: 0 15px 15px;
  background: #eee4da;
  border: 0.5px solid #bbada0;
  border-radius: 5px;
  color: #776e65;
  font-weight: bold;
}

pre {
  margin: 0;
}
.hljs {
  border-radius: 5px;
  font-weight: normal;
}
</style>
