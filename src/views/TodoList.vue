<template>
  <ContentBase>
    <div class="todo-card-container">
      <div class="todo-card-head">
        <div class="todo-card-head-left">
          <div class="plus" @click="plus">+</div>
          <div class="title">Todo List</div>
        </div>
        <div class="todo-card-head-right">
          <div class="btn-group">
            <div class="btn1" @click="notChooseAll">取消全选</div>
            <span>&nbsp;&nbsp;</span>
            <div class="btn2" @click="chooseAll">全选</div>
            <span>&nbsp;&nbsp;</span>
            <div class="btn3">全屏</div>
          </div>
        </div>
      </div>
      <hr class="todo-hr" />

      <div v-for="(item, index) in newDivs" :key="index">
        <div class="todoList">
          <div class="circle" :class="{ filled: item.isFilled }" @click="toggleCircle(index)"></div>
          <textarea name="text" id="text" placeholder="请输入TODO事件" cols="30" rows="1" v-model="item.value"
            class="text"></textarea>
          <div class="time">{{ item.time }}</div>
          <div class="btn4" @click.stop="dTodo(index)">删除</div>
        </div>
      </div>
    </div>
  </ContentBase>
</template>

<script>
import ContentBase from '../components/ContentBase';

export default {
  name: 'TodoList',
  components: {
    ContentBase,
  },

  data() {
    return {
      newDivs: [],
      isFilled: false, // 初始状态为空心
      currentTime: '', // 当前时间
    };
  },
  methods: {
    // imitation
    plus() {
      this.updateTime();
      this.newDivs.push({
        id: this.newDivs.length,
        isFilled: false,
        value: '',
        time: this.currentTime,
      });
    },
    toggleCircle(index) {
      this.newDivs[index].isFilled = !this.newDivs[index].isFilled; // 切换圆圈状态
    },
    chooseAll() {
      for (let i = 0; i < this.newDivs.length; i++) {
        this.newDivs[i].isFilled = true; // 更新每个圆圈的状态
      }
    },
    notChooseAll() {
      for (let i = 0; i < this.newDivs.length; i++) {
        this.newDivs[i].isFilled = false; // 更新每个圆圈的状态
      }
    },
    dTodo(index) {
      // console.log(id);
      // console.log(this.newDivs);
      this.newDivs.splice(index, 1);
      // const index = this.newDivs.findIndex((item) => item.id === id);
      // if (index !== -1) {
      //   this.newDivs.splice(index, 1);
      // }
    },
    updateTime() {
      const now = new Date();
      const year = now.getFullYear().toString().slice(-2); // 获取年份的后两位
      const month = (now.getMonth() + 1).toString().padStart(2, '0'); // 获取月份，并补齐两位
      const date = now.getDate().toString().padStart(2, '0'); // 获取日期，并补齐两位
      const hours = now.getHours().toString().padStart(2, '0'); // 获取小时，并补齐两位
      const minutes = now.getMinutes().toString().padStart(2, '0'); // 获取分钟，并补齐两位

      this.currentTime = `${year}-${month}-${date} ${hours}:${minutes}`; // 更新当前时间
    },
  },
};
</script>

<style scoped>
/* 模仿 */
.todo-card-container {
  background-color: rgb(54, 53, 77);
  width: 600px;
  height: 400px;
  padding: 20px;
  border-radius: 5px;
  box-shadow: 2px 2px 5px rgb(54, 53, 77);
  overflow: auto;
}

.todo-card-container::-webkit-scrollbar {
  width: 0px;
}

.todo-card-head {
  width: 560px;
  height: 40px;
  /* background-color: lightblue; */
}

.plus {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  background-color: #938ef5;
  color: white;
  line-height: 40px;
  font-size: 30px;
  float: left;
  cursor: pointer;
}

.title {
  width: 120px;
  height: 40px;
  color: white;
  line-height: 40px;
  font-size: 20px;
  font-weight: bold;
  margin-left: 10px;
  float: left;
  text-align: start;
}

.btn-group {
  width: 230px;
  height: 26px;
  color: white;
  font-size: 12px;
  line-height: 25.5px;
  margin-top: 7px;
}

.btn1 {
  width: 78px;
  background-color: #33b752;
  border-radius: 5px;
  margin: 0, 5px;
  padding: 5px, 15px;
  float: right;
  cursor: pointer;
}

.btn2 {
  width: 54px;
  background-color: #f61d25;
  border-radius: 5px;
  margin: 0, 5px;
  padding: 5px, 15px;
  cursor: pointer;
}

.btn3 {
  width: 54px;
  background-color: #2080f0;
  border-radius: 5px;
  margin: 0, 5px;
  padding: 5px, 15px;
  cursor: pointer;
}

.todo-hr {
  color: white;
  height: 20px;
  margin-top: 20px;
  margin-bottom: 8px;
  width: 100%;
}

.todoList {
  width: 100%;
  height: 60px;
  background-color: #4a4a5f;
  border-radius: 5px;
  box-shadow: 2px 2px 5px black;
  color: white;
  padding: 10px;
  margin-bottom: 10px;
  float: left;
}

.circle {
  width: 20px;
  height: 20px;
  border: 1px solid white;
  border-radius: 50%;
  cursor: pointer;
  margin: 10px 20px 10px 5px;
  float: left;
}

.filled {
  background-color: white;
}

.text {
  background-color: #4a4a5f;
  border-bottom: 1px solid white;
  border-top: none;
  border-left: none;
  border-right: none;
  color: white;
  float: left;
  margin-top: 6px;
  overflow: hidden;
  resize: none;
  outline: none;
}

.time {
  float: left;
  margin-left: 15px;
  margin-top: 7px;
}

.btn4 {
  width: 36px;
  height: 20px;
  background-color: #f61d25;
  border-radius: 5px;
  margin-top: 10px;
  margin-left: 10px;
  padding: 5px, 15px;
  font-size: 12px;
  float: left;
  cursor: pointer;
}
</style>
