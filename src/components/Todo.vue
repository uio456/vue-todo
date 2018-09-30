<template>
  <div class="container" id="app">
    <h1 class="text-center">To Do List</h1>
    <div class="panel panel-info">
      <div class="panel-heading">
        <h3 class="panel-title">事項清單</h3>
      </div>
      <!-- Add new todo -->
      <div class="panel-body">
        <form>
          <label>Add new to-do</label>
          <div class="input-group">
            <input type="text_area" id="new-todo" class="form-control" v-model="newTodo" @keypress.enter.prevent="createTodo" />
            <!--add @v-model="newTodo" on input-->
            <div class="input-group-btn">
              <button id="create-todo" class="btn btn-default" type="button" @click="createTodo">Create</button>
              <!--add @click(newTodo) on button-->
            </div>
          </div>
        </form>  
      </div>

      <!-- Todo List -->
      <table class="my-table table table-hover">
        <tbody id="todolist">
          <!--use v-for to iterate todos-->
          <tr v-for="(item, index) in todos">
            <td class="my-pointer">
              <span class="toggle-todo my-font glyphicon" v-bind:class="{
   'glyphicon-unchecked': !item.completed, 
  'glyphicon-check':item.completed }" @click="item.completed = !item.completed"></span>
            </td>
            <td class="my-title">
              <p class="title my-font" :class="{'job-done':item.completed}">
                {{item.title}},
                {{item.completed}}
                <!--show the item in todos-->
              </p>
            </td>
            <td class="my-operation">
              <span class="delete-todo my-btn my-btn-transparent text-danger glyphicon glyphicon-trash" @click="deleteTodo(index)"></>
            </td>
          </tr>
          <!-- v-for end -->
        </tbody>
      </table>
      
    </div>
      <h4 id="end" class="text-center"></h4>
    </div>
</div>
</template>
<script>
  export default {
    name: 'Todo',
    data: function() {
      return {
        todos: [],
        newTodo:''
        //     newTodo 綁定在input create button 上
      };
    },
    methods: {
      createTodo: function() {
        if(!this.newTodo){
         reture 
        }
        this.todos.push({
          title:this.newTodo,
          completed: false
        });
        this.newTodo = '';
      },
      deleteTodo: function(index) {
        this.todos.splice(index, 1);
      }
    }
  };

</script>

<style>
  a:hover {
  text-decoration: none;
}

.panel-heading .accordion-toggle:after {
  /* symbol for "opening" panels */
  font-family: 'Glyphicons Halflings';  /* essential for enabling glyphicon */
  content: "\e114";    /* adjust as needed, taken from bootstrap.css */
  float: right;        /* adjust as needed */
  color: grey;         /* adjust as needed */
}
.panel-heading .accordion-toggle.collapsed:after {
  /* symbol for "collapsed" panels */
  content: "\e080";    /* adjust as needed, taken from bootstrap.css */
}

/* ===== 預設 ===== */

.my-btn {
  padding: 0;
  border: 0;
  margin: 0;
}

.my-btn-transparent {
  background: transparent;
}

.my-pointer {
  cursor: pointer;
}

.my-font {
  font-size: 18px;
}

/* ===== 新增 ===== */
.my-create .input-group-addon button {
  width: 50px;
  height: 44px;
}

textarea {
  overflow: hidden;
  resize: none;
}


/* ===== 表格 ===== */

/* 第一欄 狀態 */

.my-table td:first-child {
  width: 30px;
  vertical-align: middle;
}

.my-pointer span {
  width: 30px;
  height: 34px;
  line-height: 34px;
  text-align: center;
}

/* 第二欄 */

.title {
  margin: 10px;
}
.my-style-done-true {
  color: #aaa;
  text-decoration: line-through;
}

.my-status-edit-true {
  display: none;
}

.my-update .input-group-addon button {
  width: 35px;
  height: 32px;
}


/* 第三欄 操作 */

.my-table td:last-child {
  width: 80px;
  vertical-align: middle;
}

.my-operation span {
  width: 30px;
  height: 34px;
  line-height: 34px;
  text-align: center;
}

.job-done {
  text-decoration: line-through
}

</style>