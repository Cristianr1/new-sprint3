<template>
  <div>
    <div class="header">
      <nav class="navbar navbar-dark bg-dark">
        <a class="navbar-brand" href="/profile">Mecanizados Group</a>
        <ul class="nav navbar-nav navbar-right">
          <button class="btn btn-danger navbar-btn" v-on:click="logout">Cerrar sesión</button>
        </ul>
      </nav>
    </div>
    <br/>
    <div class="container">
      <form action="" class="form-horizontal">
        <div class="form-group left">
          <label class="control-label col-sm-2 ">Nombre</label>
          <div class="card-text left">
            <label type="text" class="form-control" name="name" id="nombre">{{form.name}}</label>
          </div>
        </div>
        <div class="form-group left">
          <label class="control-label col-sm-2 ">Dirección</label>
          <div class="card-text left">
            <label type="text" class="form-control" name="address" id="address">{{form.address}}</label>
          </div>
        </div>
        <div class="form-group left">
          <label class="control-label col-sm-2 ">Tarea</label>
          <div class="card-text left">
            <label type="text" class="form-control" name="task" id="tarea">{{form.task}}</label>
          </div>
        </div>
        <div class="row">
          <div class="form-group col-sm-6 left">
            <label class="control-label col-sm-2 ">Correo</label>
            <div class="card-text sm-w left">
              <label type="text" class="form-control" name="email" id="email">{{form.email}}</label>
            </div>
          </div>
          <div class="form-group col-sm-6 left">
            <label class="control-label col-sm-2 ">Telefono</label>
            <div class="card-text sm-w left">
              <label type="text" class="form-control" name="mobile" id="mobile">{{form.mobile}}</label>
            </div>
          </div>
        </div>
        <div class="row">
          <div class="form-group col-sm-6 left">
            <label class="control-label col-sm-2 ">Rol</label>
            <div class="card-text sm-w left">
              <label type="text" class="form-control" name="rol" id="rol">{{form.rol}}</label>
            </div>
          </div>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Profile",
  components: {},
  data:function (){
    return{
      username:"",
      form:{
        "username": "",
        "password": "",
        "rol": "",
        "address":"",
        "task": null,
        "email": null,
        "mobile": null,
        "logged_in": false,
        "name":"",
      }
      }

    },
  methods:{
    logout: function (){
      localStorage.removeItem("username")
      this.$router.push("/")
    }
  },
  mounted: function (){
    this.username = localStorage.username
    axios.get("https://gestion-cliente.herokuapp.com/employee/data/" + this.username).then(data =>{
      this.form.username = data.data.username
      this.form.password = data.data.password
      this.form.rol = data.data.rol
      this.form.address = data.data.address
      this.form.task = data.data.task
      this.form.email = data.data.email
      this.form.mobile = data.data.mobile
      this.form.logged_in = data.data.logged_in
      this.form.name = data.data.name
      console.log(this.form)
    })
  }
}
</script>

<style scoped>
body{
  margin: 0;
}

.container{
  align-items: center;
  height: 80%;
}
.left{
  text-align: left;
}

.sm-w{
  max-width: 100%;
}
</style>