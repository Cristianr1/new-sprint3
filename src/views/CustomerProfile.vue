<template>
  <div>
    <div class="header">
      <nav class="navbar navbar-dark bg-dark">
        <a class="navbar-brand" href="/profile">Mecanizados Group - {{form.rol}}</a>
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
            <label type="text" class="form-control" name="name" id="nombre">{{form.username}}</label>
          </div>
        </div>
        <div class="form-group left">
          <label class="control-label col-sm-2 ">Dirección</label>
          <div class="card-text left">
            <label type="text" class="form-control" name="address" id="address">{{form.address}}</label>
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
            <label class="control-label col-sm ">Estado Factura</label>
            <div class="card-text sm-w left">
              <label type="text" class="form-control" name="bill" id="bill">{{form.bill}}</label>
            </div>
          </div>
        <div class="form-group col-sm-6 left">
            <label class="control-label col-sm-2 ">Factura</label>
            <div class="card-text sm-w left">
              <label type="text" class="form-control" name="invoice" id="invoice">{{form.invoice}}</label>
            </div>
          </div>
        </div>
        <div class="row">
          <div class="form-group col-sm-6 left">
             <button class="btn-payment" v-on:click="payBill">Pagar Factura</button>
          </div>
        <div class="form-group col-sm-6 left">
             <button class="btn-generate" v-on:click="generateInvoice">Generar Factura</button>

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
            "rol": "",
            "address":"",
            "email": null,
            "mobile": null,
            "invoice": 0,
            "bill": ""
        }
        }

        },
    methods:{
    logout: function (){
        localStorage.removeItem("username")
        this.$router.push("/")
    },

    generateInvoice() {
        axios.put('https://gestion-cliente.herokuapp.com/customer/invoice/', { name: this.username })
    },

    payBill() {
        axios.put('https://gestion-cliente.herokuapp.com/customer/payment/', { name: this.username })
    },
    },
    mounted: function (){
        this.username = localStorage.username
        axios.get("https://gestion-cliente.herokuapp.com/customer/data/" + this.username).then(data =>{
        this.form.username = data.data.username
        this.form.rol = data.data.rol
        this.form.address = data.data.address
        this.form.email = data.data.email
        this.form.mobile = data.data.mobile
        this.form.invoice = data.data.invoice
        this.form.bill = data.data.isPayment ? "Pagada" : "Sin Pagar"
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

.btn-payment{
    background-color: green;
    color: white;
    height: 60px;
    width: 180px;
    border-radius: 10px;
}

.btn-generate{
    color: green;
    background-color: white;
    height: 60px;
    width: 180px;
    border-radius: 10px;
}
</style>