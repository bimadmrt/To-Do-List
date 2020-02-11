<template>
  <div class="container">
    <div class="header">
    <h1>YANG HARUS DIKERJAKAN OLEH BIMA</h1>
    <div class="item-logo">
      <img alt="starbuck" src="../assets/starbucks.png">
      <h1>JANCOK AKEH JANCOK</h1>
      <br />
    </div>
    </div>
      <div class="container">
      <div class="todo-list">
        <div class="item" v-for="(item, index) in todoList" :key="index">
          <div class="card-todo">
            <div class="col-8">
            <h2 style="text-align: center">{{item.task}}</h2>
            <p style="text-align: center">{{item.courses}} Deadline  {{item.deadline}}</p>
            <p style="text-align: center">{{item.description}}</p>
            </div>
          <div class="col-4">
            <button class="btn-remove" @click="removeData(item)" >HAPUS</button>
            </div>
          </div>
        </div>
        </div>
    </div>
    <div class="tambah-data">
      <div class="form-tambah">
      <h2>Masukan Masalahmu Disini</h2>
      <form @submit.prevent="addData">
        <input type="text" placeholder="Tugas" v-model="taskData"/>
        <br/>
        <input type="text" placeholder="Mata Kuliah" v-model="coursesData"/>
        <br/>
        <input type="text" placeholder="Deadline" v-model="deadlineData"/>
        <br/>
        <input type="text" placeholder="Description" v-model="descriptionData"/>
        <br />
        <button class="btn-add" @click="addData">Masuk Pak Eko</button>
      </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data: () => ({
    taskData: '',
    coursesData: '',
    deadlineData: '',
    descriptionData: '',
    todoList: [],
  }),
  created() {
    this.loadlocalStorage();
  },
  watch: {
    todoList() {
      localStorage.setItem('todoList', JSON.stringify(this.todoList));
    },
  },
  methods: {
    addData() {
      if (this.taskData !== '') {
        const date = new Date();
        const dataTask = {
          id: date.getTime(),
          task: this.taskData,
          courses: this.coursesData,
          deadline: this.deadlineData,
          description: this.descriptionData,
          complete: false,
          show: false,
        };
        this.todoList.push(dataTask);
      }
      this.taskData = '';
      this.coursesData = '';
      this.deadlineData = '';
      this.descriptionData = '';
    },
    removeData(item) {
      const index = this.todoList.findIndex((Element) => Element.id === item.id);
      this.todoList.splice(index, 1);
    },
    loadlocalStorage() {
      const ls = JSON.parse(localStorage.getItem('todoList'));
      if (ls == null) {
        return;
      }
      this.todoList = ls;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.container {
  display: block;
  text-align: center;
  grid-column: 1/3;
  grid-template-columns: repeat(1, 1fr);
  margin: 10px;
}
.item-logo {
  float: center;
  margin-right: 20px;
  margin-bottom: 20px;
}
.header{
  text-align: center;
  grid-column: 1/3;
  border:5px solid grey;

}
.tambah-data {
  display: inline-block;
  width: 550px;
  text-align: center
}
.form-tambah {
  box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
  padding-top: 10px;
}
.todo-list {
  display: inline-block;
  width: 750px;
}
input[type=text] {
  height: 30px;
  margin: 5px;
  padding: 5px;
  cursor: pointer;
  transition: 0.3s;
  width: 450px;
}
input[type=text]:focus {
  border: 2px solid dimgrey;
  border-radius: 0px;
}
.btn-add{
    background-color: transparent;
    color:black;
    border: 2px solid black;
    border-radius: 0px;
    text-align: center;
    margin: 5px 2px;
    padding: 10px 15px;
    cursor: pointer;
    transition: 0.3s;
    margin: 20px;
    width: 300px;
}
.btn-add:hover{
    background-color: black;
    color: white;
}
.card-todo {
    box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
    transition: 0.3s;
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    grid-auto-rows: minmax(10px, auto);
    margin-bottom: 20px;
    background-color: #f5f5f5;
}
.col-8 {
  padding-left: 10px;
  width: 600px;
}
.card-todo:hover {
    box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2);
}
.btn-remove{
    background-color: transparent;
    color:red;
    border: 2px solid red;
    border-radius: 0px;
    text-align: center;
    margin: 5px 2px;
    padding: 10px 15px;
    cursor: pointer;
    transition: 0.3s;
    margin: 20px;
}
.btn-remove:hover{
    background-color: red;
    color: white;
}
</style>