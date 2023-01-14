<script setup>
import Header_Perspective from './components/header.vue'
import RUI_Content from './components/RUI_Content.vue'
//import TEST from './components/test.vue'
</script>

<template>
  <header id="ha-header" :class="['ha-header',classObject]">
      <Header_Perspective/>
  </header>
  <RUI_Content/>
</template>
<script>
export default {
 // props: {},
  data() {
  return {
    classObject:'larger'
  }
},

  mounted() {
    // 监听滚动事件
    window.addEventListener('scroll', this.onScroll, false)
  },
  destroy() {
    // 必须移除监听器，不然当该vue组件被销毁了，监听器还在就会出错
    window.removeEventListener('scroll', this.onScroll)
  },
  methods: {
    // 滚动监听器
    onScroll() {
      // 获取所有锚点元素
      const navsection = document.querySelectorAll('section')
      // 所有锚点元素的 offsetTop
      const offsetTopArr = []
      navsection.forEach(item => {
        offsetTopArr.push(item.offsetTop)
      })
      // 获取当前文档流的 scrollTop
      const scrollTop = document.documentElement.scrollTop || document.body.scrollTop
      // 定义当前点亮的导航下标
      
      if (scrollTop < 702)
      {
        this.classObject  ='larger'
       
      }
      if (scrollTop > 703)
      {
        this.classObject  ='small'
      }
      if (scrollTop > 1403)
      {
        this.classObject  ='hide'
      }
      if (scrollTop > 2003)
      {
        this.classObject  ='show'
      }
      if (scrollTop > 2703)
      {
        this.classObject  ='subshow'
      }
      if (scrollTop > 3403)
      {
        this.classObject  ='show'
      }
       if (scrollTop > 4003)
      {
        this.classObject  ='shrink'
      }
       if (scrollTop > 4703)
      {
        this.classObject  ='rotateBack'
      }
       if (scrollTop > 5103)
      {
        this.classObject  ='rotate'
      }
      if (scrollTop > 5703)
      {
        this.classObject  ='rotateBack'
      }
       if (scrollTop > 6203)
      {
        this.classObject  ='color'
      }
       if (scrollTop > 6803)
      {
        this.classObject  ='fullscreen'
      }
        
    },
  }
}
</script>