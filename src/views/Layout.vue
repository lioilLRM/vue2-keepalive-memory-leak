<template>
  <div>
    <h1>Layout</h1>
    <div class="box">
      <p>二级路由</p>
      <router-link :to="{ name: 'A' }">A</router-link>
      <br>
      <router-link :to="{ name: 'B' }">B</router-link>
    </div>

    <div class="box">
      <p>三级路由</p>
      <router-link :to="{ name: 'AA' }">Page1</router-link>
      <br>
      <router-link :to="{ name: 'BB' }">Page2</router-link>
    </div>

    <div class="box">
      <button @click="includeRemove()">清理keepalive缓存</button>
      <button @click="showRoutes">查看route</button>
      <br>
      <router-link to="/home">Home</router-link>
      <br>
    </div>

    <h1>keep-alive</h1>
    缓存页面：{{ include }}
    <keep-alive :include="include">
      <router-view ref="alive" />
    </keep-alive>
  </div>
</template>

<script>
export default {
  name: 'Layout',
  data() {
    return {
      include: []
    }
  },
  watch: {
    '$route'(val) {
      const name = val.meta.name
      if (name && !this.include.includes(name)) {
        this.include.push(name)
      }
    }
  },
  mounted() {},
  methods: {
    includeRemove() {
      this.include = []
      // 为啥vue-router不开放直接获取nameMap的接口 淦
      // const routes = this.$router.getRoutes()
      // // console.log('🚀 ~ includeRemove ~ routes:', routes)
      // const nameMap = new Map()
      // for (let index = 0; index < routes.length; index++) {
      //   const r = routes[index]
      //   nameMap.set(r.name, r)
      // }

      // // 假设我这边获取到了当前移除的tab页签，具体代码根据具体项目实现
      // const rList = ['AA', 'BB']
      // for (let index = 0; index < rList.length; index++) {
      //   const name = rList[index]
      //   const r = nameMap.get(name)
      //   if (r) r.instances.default = undefined
      // }
    },
    showRoutes() {
      // console.log('🚀 ~ showRoutes ~ routes:', this.$router.getRoutes())
    }
  }
}
</script>
<style>
.box {
  margin-bottom: 20px;
}
</style>
