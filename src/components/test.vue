<template>
  <div>
    <!-- 内容区域 -->
    <div class="content">
      <div>
        content-0
      </div>
      <div>
        content-1
      </div>
      <div>
        content-2
      </div>
      <div>
        content-3
      </div>
      <div>
        content-4
      </div>
    </div>
    <!-- 导航区域 -->
    <ul class="navs">
      <li :class="{active: active===0}">
        content-0
      </li>
      <li :class="{active: active===1}" >
        content-1
      </li>
      <li :class="{active: active===2}">
        content-2
      </li>
      <li :class="{active: active===3}">
        content-3
      </li>
      <li :class="classObject">
        content-4
      </li>
    </ul>
  </div>
</template>

<script>
export default {
 // props: {},
  data() {
  return {
    classObject:{ 
      active: 1, 
      sort:0
    }
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
      const navContents = document.querySelectorAll('.content div')
      // 所有锚点元素的 offsetTop
      const offsetTopArr = []
      navContents.forEach(item => {
        offsetTopArr.push(item.offsetTop)
      })
      // 获取当前文档流的 scrollTop
      const scrollTop = document.documentElement.scrollTop || document.body.scrollTop
      // 定义当前点亮的导航下标
      let navIndex = 0
      for (let n = 0; n < offsetTopArr.length; n++) {
        // 如果 scrollTop 大于等于第n个元素的 offsetTop 则说明 n-1 的内容已经完全不可见
        // 那么此时导航索引就应该是n了
        if (scrollTop >= offsetTopArr[n]) {
          navIndex = n
        }
      }
      if (navIndex == 2)
      {
        this.classObject.sort  =  true
      }
      if (navIndex == 3)
      {
        this.classObject.sort  =  false
      }
        
    },
  }
}
</script>

<style scoped>
  /* 内容区的样式 */
  .content {
    background-color: white;
    width: 500px;
  }
  .content div {
    width: 100%;
    height: 600px;
    font-size: 36px;
    padding: 20px;
    background-color: #7ec384;
  }
  .content div:nth-child(2n) {
    background-color: #847ec3;
  }
  /* 导航栏的样式 */
  .navs {
    position: fixed;
    top: 80px;
    left: 700px;
    background-color: #efefef;
  }
  .navs li {
    padding: 0 20px;
    line-height: 1.6;
    font-size: 24px;
  }
  /* 当导航被点亮后改变颜色 */
  .navs .active{
    color: #847ec3;
    background-color: #e2e2e2;
  }
</style>
