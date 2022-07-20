<template>
<h1>Welcome {{title}}!!!</h1>
    <div class="container-fluid">
        <div class="row">
            <div class="col-md-3">
            </div>
            <div class="col-md-6">
                <table class="table">
                    <thead>
                        <tr>
                            <th>#Id</th>
                            <th>Contact</th>
                            <th>Phone</th>
                            <th>Date added</th>
                            <th>Status</th>
                            <th>Actions</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="(row, index) in data" :key="row.id" v-bind:class="{'table-active' : index%2 == 0}"> <!--color de filamintercalado-->
                            <td>{{ row.id }} </td>
                            <td>{{ row.contact }}</td>
                            <td>{{ row.phone }}</td>
                            <td>{{ row.date }}</td>
                            <td>{{ row.status }}</td>
                            <td>
                                 
                                <button type="button" class="btn btn-success btn-sm" data-bs-toggle="modal" data-bs-target="#exampleModal" @click="Updaterow(index)">Update
                                </button>
                                <button type="button" class="btn btn-danger btn-sm" @click="remove(index)">Delete
                                </button>
                            </td>
                        </tr>
                    </tbody>
                </table>
            </div>
            <div class="col-mod-3">
                <button type="button" class="btn btn-primary btn-sm" @click="create()">
                    Create
                </button>
            </div>
        </div>
    </div>

    <div class="container-fluid">
        <div class="row">
            <div class="col-md-12">
                <div class="row">
                    <div class="col-md-6">
                    </div>
                    <div class="col-md-3">
                       
                        <button type="button" class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#exampleModal">
                            Add Contact
                        </button>

                       
                        <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
                            <div class="modal-dialog">
                                <div class="modal-content">
                                    <div class="modal-header"> 
                                        <h5 class="modal-title" id="exampleModalLabel">Modal title</h5>
                                        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                                    </div>
                                    <div class="modal-body">
                                        <div class="mb-3">
                                            <label for="exampleFormControlInput1" class="form-label">Id</label>
                                            <input type="text" class="form-control" id="" placeholder="id" v-model="inputId">  <!--Nombre variable-->

                                            <label for="exampleFormControlInput1" class="form-label">Contact</label>
                                            <input type="text" class="form-control" id="" placeholder="Contact" v-model="inputContact">

                                            <label for="exampleFormControlInput1" class="form-label">Phone</label>
                                            <input type="text" class="form-control" id="" placeholder="Phone" v-model="inputPhone">

                                            <label for="exampleFormControlInput1" class="form-label">Date</label>
                                            <input type="date" class="form-control" id="" placeholder="Date" v-model="inputDate">

                                            <label for="exampleFormControlInput1" class="form-label">Status</label>
                                            <input type="text" class="form-control" id="" placeholder="Status" v-model="inputStatus">

                                        </div>
                                    </div>
                                    <div class="modal-footer">
                                        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
                                        <button type="button" class="btn btn-primary" @click="saveChanges()">Save changes</button>
                                    </div>
                                </div>
                            </div>
                        </div>
                        
                    </div>
                    <div class="col-md-3">
                    </div>
                </div>
            </div>
        </div>
	</div>
</template>

<script>
    export default{
        data(){
            return{
                data : [
                    {id: 1, contact: "Frida", phone: "4492453976", date: "15/09/2022", status: "Inactivo"},
                    {id: 2, contact: "Cecilio", phone: "4492391234", date: "13/03/2022", status: "Activo"},
                    {id: 3, contact: "David", phone: "4495559876", date: "28/12/2022", status: "Inactivo"},
                    {id: 4, contact: "Valeria", phone: "4499562341", date: "16/07/2022", status: "Activo"},
                    {id: 5, contact: "Francisco", phone: "4495015670", date: "07/05/2022", status: "Activo"}
                ],
                inputId : "",
                inputContact : "", 
                inputPhone : "",   
                inputDate : "",
                inputStatus : "",       
            
            }
        },
        methods:{
            select(id, index){
                console.log("Rowid = " + id);
                console.log("Index = " + index);

                console.log(this.data[index].contact); /*Imprimir dato */
                this.data[index].contact="Rodrigo"; /*Modificar dato */
                console.log(this.data[index].contact); /*Mostrar nuevo dato */
            },
            remove(index){
                console.log(index);
                this.data.splice(index, 1);
            },
            create(){ /*dato estatico*/
                this.data.push({id: 6, contact: "Maria", phone: "4492050308", date: "15/07/2022", status: "Inactivo"});
            },
            saveChanges(){ /*Metodo para guardar datos no estaticos (guardarlos desde el modal siempre y cuando no este vacio)*/
                if (this.inputId !="" && this.inputContact !="" && this.inputPhone !="" && this.inputDate !="" && this.inputStatus) {
                this.data.push({id: this.inputId, contact: this.inputContact, phone: this.inputPhone, date: this.inputDate, status: this.inputStatus});
                this.inputId = "";
                this.inputContact = "";
                this.inputPhone = "";  
                this.inputDate = "";
                this.inputStatus = ""; 
                } else{
                    alert("All fields are requiered")
                }
            },
            Updaterow(index){
                this.inputId = this.data[index].id;
                this.inputContact = this.data[index].contact;
                this.inputPhone = this.data[index].phone;   
                this.inputDate = this.data[index].date;
                this.inputStatus = this.data[index].status;
            }
        },
        created(){
            const headers = {"Content-Type":"appliation/json"}
            fetch("https://reqres.in/api/products/3")
                .then(async response=> await response.json)
                .then(data =>(console.log(data)));
        },
        props: {
            title: String
        }
    }

</script>