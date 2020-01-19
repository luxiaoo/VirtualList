<template>
  <!-- 可视区域容器 -->
  <div ref="list" class="infinite-list-container" @scroll="scrollEvent($event)">
    <div class="infinite-list-phantom" :style="{height: listHeight+'px'}"></div>
    <!-- 列表渲染区域 -->
    <div class="infinite-list" :style="{transform: getTransform}">
      <div
        ref="items"
        class="infinite-list-item"
        v-for="item in visibleData"
        :key="item.id"
        :style="{height:itemSize + 'px',lineHeight: itemSize + 'px'}"
      >{{item.value}}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWord",
  props: {
    listData: {
      type: Array,
      default: () => {}
    },

    itemSize: {
      type: Number,
      default: 200
    }
  },

  computed: {
    //列表总长度
    listHeight() {
      return this.listData.length * this.itemSize;
    },

    //可显示的列表项数
    visibleCount() {
      return Math.ceil(this.screenHeight / this.itemSize);
    },

    //偏移量对应的style 向上滚动时，容器也会跟随一块儿上移，将偏移量再加回来，用移动给他移回去

    getTransform(){
      return `translate3d(0,${this.startOffset}px,0)`;
    },

    //获取真实显示列表数据
    visibleData() {
      return this.listData.slice(
        this.start,
        Math.min(this.end, this.listData.length)
      );
    }
  },

  mounted() {
    this.screenHeight = this.$el.clientHeight;
    this.start = 0;
    this.end = this.start + this.visibleCount;
  },

  data() {
    return {
      screenHeight: 0,
      startOffset: 0,
      start: 0,
      end: null
    };
  },

  methods: {
    scrollEvent() {
      let scrollTop = this.$refs.list.scrollTop;
      this.start = Math.floor(scrollTop / this.itemSize);
      this.end = this.start + this.visibleCount;
      this.startOffset = scrollTop - (scrollTop % this.itemSize);
      
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->

<style scoped>
.infinite-list-container {
  height: 100%;
  overflow: auto;
  position: relative;
  -webkit-overflow-scrolling: touch;
}

.infinite-list-phantom {
  position: absolute;
  left: 0;
  top: 0;
  right: 0;
  z-index: -1;
}

.infinite-list {
  left: 0;
  right: 0;
  top: 0;
  position: absolute;
  text-align: center;
}

.infinite-list-item {
  padding: 10px;
  color: #555;
  box-sizing: border-box;
  border-bottom: 1px solid #999;
}

.infinite-list-container {
  height: 100%;
  overflow: auto;
  position: relative;
  -webkit-overflow-scrolling: touch;
}

.infinite-list-phantom {
  position: absolute;
  left: 0;
  top: 0;
  right: 0;
  z-index: -1;
}

.infinite-list {
  left: 0;
  right: 0;
  top: 0;
  position: absolute;
  text-align: center;
}

.infinite-list-item {
  padding: 10px;
  color: #555;
  box-sizing: border-box;
  border-bottom: 1px solid #999;
}
</style>