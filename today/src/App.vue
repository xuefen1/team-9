<template>
  <div id="app">
    <ul>
      <li class="checked-item" v-for="(item,index) in goods" :key="index" @click="singleSelect(item,index)">
        <input type="checkbox" :checked="item.checked">
        {{item.name}}
      </li>
    </ul>
    <div>
       <span @click="allSelect">
        <input type="checkbox" :checked="isAllSelected">
        <button>全选</button>
      </span>
      <span class="checked-count" v-if='checkedId.length>0'>已选择:{{checkedId.length}}项</span>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      goods: [
        {
          id: 1,
          name: "选项1",
          checked: false
        },
        {
          id: 2,
          name: "选项2",
          checked: false
        },
        {
          id: 3,
          name: "选项3",
          checked: false
        },
        {
          id: 4,
          name: "选项4",
          checked: false
        },
        {
          id: 5,
          name: "选项5",
          checked: false
        },
        {
          id: 6,
          name: "选项6",
          checked: false
        }
      ]
    };
  },
  methods: {
     //全选全不选
    allSelect() {
      let checked = true;
      //全选
      if (this.isAllSelected) {
          checked=false;
      }
      this.goods=this.goods.map((el)=>{
         el.checked = checked;
         return el;
      })
    },
    //单选
    singleSelect(item,index){
       item.checked = !item.checked;
        this.goods.splice(index,1,item);
    }
  },
  computed: {
    //是否全选
    isAllSelected(){
      return this.goods.every((el)=>{
         return el.checked;
      })
    },
     //选中id
    checkedId(){
       let filterArr =this.goods.filter((el)=>{
           return el.checked;
       });
       return filterArr.map((el)=>{
          return el.id
       })
    }
  }
};
</script>

<style>
#app {
}
</style>
