
    <link rel="stylesheet" href="bootstrap.min.css">
    <script src="jquery-3.2.1.min.js"></script>
    <script src="bootstrap.min.js"></script>
    <script src="vue.min.js"></script>

    <script>
        window.onload=function(){
            new Vue({
                el:'.container',
                data:{
                    users:[
                        {name:'tom',age:24,email:'tom@itany.com'},
                        {name:'jack',age:24,email:'jack@itany.com'}
                    ],
                    user:{},
                    nowIndex:-1,
                },
                methods:{
                    addUser:function (){
                        this.users.push(this.user)
                        this.user={}
            },
                    delUser:function (){
                        if(this.nowIndex===-1){
                            this.users=[]
                        }
                        else{
                            this.users.splice(this.nowIndex,1)
                        }

                    }
                },

            })
        }
    </script>
    <div class="container">
        <h2 class="text-center">添加用户</h2>
        <form class="form-horizontal">
            <div class="form-group">
                <label for="name" class="control-label col-sm-2 col-sm-offset-2">姓名:</label>
                <div class="col-sm-6">
                    <input type="text" class="form-control" id="name" v-model="user.name" placeholder="请输入姓名">
                </div>
            </div>
            <div class="form-group">
                <label for="age" class="control-label col-sm-2 col-sm-offset-2">年龄:</label>
                <div class="col-sm-6">
                    <input type="text" class="form-control" id="name" v-model="user.age" placeholder="请输入年龄">
                </div>
            </div>
            <div class="form-group">
                <label for="email" class="control-label col-sm-2 col-sm-offset-2">邮箱:</label>
                <div class="col-sm-6">
                    <input type="text" class="form-control" id="email" v-model="user.email" placeholder="请输入邮箱">
                </div>
            </div>
            <div class="form-group text-center">
                <input type="button" value="添加" class="btn btn-primary" v-on:click="addUser">
                <input type="button" value="重置" class="btn btn-primary" v-on:click="delUser">
            </div>
        </form>
        <br>
        <table class="table table-bordered table-hover">
            <caption class="h3 text-center text-info">用户列表</caption>
            <thead>
                <tr>
                    <th  class="text-center">序号</th>
                    <th  class="text-center">姓名</th>
                    <th  class="text-center">年龄</th>
                    <th  class="text-center">邮箱</th>
                    <th  class="text-center">操作</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(user,index) in users" class="text-center">
                    <td>{{index+1}}</td>
                    <td>{{user.name}}</td>
                    <td>{{user.age}}</td>
                    <td>{{user.email}}</td>
                    <td>
                        <button class="btn btn-danger btn-sm" data-toggle="modal" data-target="#del" v-on:click="nowIndex=index">删除</button>
                    </td>

                </tr>
                <td class="text-right" colspan="5">
                    <button class="btn btn-danger btn-sm" data-toggle="modal" data-target="#del" v-on:click="nowIndex=-1">删除所有</button>
                </td>
            </tbody>
        </table>
        <div class="modal" id="del">
            <div class="modal-dialog">
                <div class="modal-content">
                    <div class="modal-header">
                        <button class="close" data-dismiss="modal">
                            <span>&times</span>
                        </button>
                        <h4 class="modal-title" v-show="nowIndex!==-1">确定要删除用户:{{users[nowIndex]?users[nowIndex].name:''}}么？</h4>
                        <h4 class="modal-title" v-show="nowIndex===-1">确定要删除所有用户么？</h4>
                    </div>
                    <div class="modal-body text-center">
                        <button class="btn btn-primary" data-dismiss="modal">取消</button>
                        <button class="btn btn-primary" data-dismiss="modal" v-on:click="delUser">确认</button>
                    </div>
                </div>
            </div>
        </div>
    </div>

