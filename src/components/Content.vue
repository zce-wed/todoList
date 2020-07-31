<!--  -->
<template>
  <div class>
    <!-- 内容顶部输入框开始 -->
    <div class="content-top">
      <div :class="['content-top-left',{allCheck:allCheckLabel}]"
        @click='allCheckFunc'
      >></div>
      <div class="content-top-right">
        <input type="text" 
        v-model="inputVal"
        @keyup.enter.stop="saveTode"
        placeholder="what needs to be done ?" />
      </div>
    </div>
    <!-- 内容顶部输入框结束 -->
    <!-- 中间列表项的开始 -->
    <div class="app-content-middle">
      <section class="content-middle-item" v-for="item,index in filterTodos" :key="item.id">
        <section class="content-middle-left">
          <input type="checkbox" v-model="item.completed" />
        </section>
        <section class="content-middle-mid" @dblclick="editTodo(index)">
           
            <span :class="[{hidden:edit_index==index},{complete:item.completed}]"> {{item.content}}</span>
            <input type="text" 
            @blur="saveEditTodo(index)"
            v-model="item.content"  :class="{hidden:edit_index!=index}">
        </section>
        <section class="content-middle-right"
        @click.stop='removeTodo(index)'
        >X</section>
      </section>
    </div>
    <!-- 中间列表项的结束-->
    <!-- 底部功能栏开始 -->
        <div class="app-content-bottom">
            <div class="content-bottom-left">剩下{{remaining}}项</div>
            <div class="content-bottom-middle">
                <a href="#/all">all</a>
                <a href="#/active">active</a>
                <a href="#/complete">complete</a>
            </div>
            <div class="content-bottom-right" @click.stop="cleanCompletedFunc">
                清除已完成
            </div>
        </div>
    <!-- 底部功能栏结束 -->
  </div>
</template>

<script>
//这里可以导入其他文件（比如：组件，工具js，第三方插件js，json文件，图片文件等等）
//例如：import 《组件名称》 from '《组件路径》';

export default {
  //import引入的组件需要注入到对象中才能使用
  components: {},
  data() {
    //这里存放数据
    return {
      todos: [
        {
          id: 1,
          content: "需求分析",
          completed: true,
        },
        {
          id: 2,
          content: "功能开发",
          completed: false,
        },
        {
          id: 3,
          content: "产品测试",
          completed: false,
        },
        {
          id: 4,
          content: "产品上线",
          completed: false,
        },
      ],
      inputVal:'',
      visibility:'all',
      allCheckLabel:false,
      edit_index:-1 //代表现在在编辑哪一行
    };
  },
  //监听属性 类似于data概念
  computed: {
    filterTodos: function () {
      if(this.visibility == 'all'){
         return this.todos;
      }else if(this.visibility =='active'){
          return this.todos.filter((v,i)=>{
              if(!v.completed){
                  return true
              }else{
                return false
              }

          })
      }else{
        return this.todos.filter((v,i)=>{
          if(v.completed){
             return true
          }else{
            return false
          }
        })
      }
     
    },
    remaining:function(){
        let remainTodos = this.todos.filter((v,i)=>{
            if(!v.completed){
                return true
            }else{
                return false
            }
           
        })
         return remainTodos.length;
    }
  },
  //监控data中的数据变化
  watch: {},
  //方法集合
  methods: {
      saveTode:function(){
          let inputVal = this.inputVal;
          if(inputVal.trim()===''){
              alert('输入不能为空')
              return false
          }
          this.todos.push({
              id:Date.now(),
              content:inputVal,
              completed:false
          })
      },
      allCheckFunc:function(){
        this.todos.forEach((v,i) => {
            v.completed=true
        })
        this.allCheckLabel=true
      },
      removeTodo:function(index){
          this.todos.splice(index,1)
      },
      editTodo:function(index){
          this.edit_index=index
      },
      saveEditTodo:function(index){
          this.edit_index = -1;
      },
      cleanCompletedFunc:function(){
          let filterTodos = this.todos.filter((v,i)=>{
              if(!v.completed){
                  return true 
              }else{
                  return false
              }
          })
          this.todos = filterTodos
      }
  },
  //生命周期 - 创建完成（可以访问当前this实例）
  created() {},
  //生命周期 - 挂载完成（可以访问DOM元素）
  mounted() {
      let _this=this;
      window.addEventListener('hashchange',function(){
          let visibility = location.hash.replace('#/','');
          _this.visibility = visibility
      })
  },
  beforeCreate() {}, //生命周期 - 创建之前
  beforeMount() {}, //生命周期 - 挂载之前
  beforeUpdate() {}, //生命周期 - 更新之前
  updated() {}, //生命周期 - 更新之后
  beforeDestroy() {}, //生命周期 - 销毁之前
  destroyed() {}, //生命周期 - 销毁完成
  activated() {}, //如果页面有keep-alive缓存功能，这个函数会触发
};
</script>
<style lang='less' scoped>
.hidden{
    display: none;
}
.content-top {
  display: flex;
  justify-content: space-between;
  .allCheck{
      color: red;
  }
  .content-top-left {
    font-size: 20px;
    flex: 1;
    text-align: center;
    transform: rotate(90deg);
  }

  .content-top-right {
    flex: 8;
    input {
      height: 26px;
      width: 90%;
      font-size: 16px;
    }
  }
}
.app-content-middle {
  .content-middle-item {
    line-height: 50px;
    display: flex;
    .content-middle-left {
      // background-color: salmon;
      text-align: center;
      flex: 1;
      input {
      }
    }

    .content-middle-mid {
        .complete{
            text-decoration: line-through;
        }
      flex: 8;
    }

    .content-middle-right {
      flex: 1;
      display: none;
    }
  }
}
.content-middle-item:hover {
  .content-middle-right {
    display: block;
  }
}
.app-content-bottom {
    height: 50px;
    align-items: center;
    display: flex;
    justify-content: space-between;
  .content-bottom-left {

  }

  .content-bottom-middle {
    a {
        display: inline-block;
        margin-left: 10px;
    }
  }

  .content-bottom-right {

  }
}
</style>