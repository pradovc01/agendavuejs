<template>
    <div class="about">
        <h5 class="mb-5 mt-5"> Agenda de Contactos</h5>
        
        <div class="mb-3">
                <div class="input-group">
                    <span class="input-group-text" id="description-search-text"><i class="bi bi-search"></i> Filtro: </span>                    
                        <input type="search"  class="form-control" v-model="search" placeholder="Buscar contacto..." @search="toSearch= $event.target.value"> 
                </div>
            </div>
        <div class="card">
            <div class="card-body" >
                <form @submit.prevent="save_contact()">
                    <table class="table table-striped">
                        <thead>                   
                        <tr>
                            <th>ID</th>
                            <th>Nombre</th>
                            <th>Email</th>
                            <th>Address</th>
                            <th>Phone</th>
                            <th>Country</th>
                            <th>City</th>
                        </tr>
                        <tr>
                            <td><button type="submit" class="btn btn-primary">Agregar</button></td>
                            <td><input type="text" class="form-control" id="name" v-model="new_contact.name"/></td>
                            <td><input type="text" class="form-control" id="email" v-model="new_contact.email"/></td>
                            <td><input type="text" class="form-control" id="address" v-model="new_contact.address"/></td>
                            <td><input type="text" class="form-control" id="phone" v-model="new_contact.phone"/></td>
                            <td><input type="text" class="form-control" id="country" v-model="new_contact.country"/></td>                        
                            <td><input type="text" class="form-control" id="city" v-model="new_contact.city"/></td>
                        </tr>                    
                        </thead>
                        <tbody>
                        <tr v-for="contact in get_contacts()" :key="contact.id">
                            <td>{{ contact.id }}</td>
                            <td>{{ contact.name }}</td>                
                            <td>{{ contact.email }}</td>
                            <td>{{ contact.address }}</td>
                            <td>{{ contact.phone }}</td>
                            <td>{{ contact.country }}</td>
                            <td>{{ contact.city }}</td>
                            <td><button type="button" class="btn btn-danger btn-sm" @click="remove(contact.id)"><i class="bi bi-trash3"></i></button></td>
                            <td><button type="button" class="btn btn-info btn-sm"  data-bs-toggle="modal" data-bs-target="#editModal" @click="edit(contact.id)"><i class="bi bi-pen"></i></button></td>
                        </tr>
                        </tbody>
                    </table>

                </form>
            </div>
        </div>

        <Modal id="editModal" :contactData="contactSelected" @close="toggleModal" @save="updateContact"/>
        

    </div>
</template>

<script>
    import Modal from '../components/modalcomponent.vue'
    export default{
        data(){
            return {
                new_contact:{
                    id:null,
                    name:"",
                    email:"",
                    address:"",
                    phone:"",
                    country:"",
                    city:""

                },
                contacts: [
                    {id: 1, name: "Alice Johnson", email: "alice.johnson@example.com", address: "123 Maple Street", phone: "123-456-7890", country: "USA", city: "New York" },
                    {id: 2, name: "Bob Smith", email: "bob.smith@example.com", address: "456 Oak Avenue", phone: "987-654-3210", country: "Canada", city: "Toronto"},
                    {id: 3, name: "Carol White", email: "carol.white@example.com", address: "789 Pine Road", phone: "555-123-4567", country: "UK", city: "London"},
                    {id: 4, name: "David Brown", email: "david.brown@example.com", address: "321 Elm Street", phone: "444-555-6666", country: "Australia", city: "Sydney"},
                    {id: 5, name: "Emily Davis", email: "emily.davis@example.com", address: "654 Spruce Lane", phone: "333-444-5555", country: "USA",city: "Los Angeles"}
                ],                
                contactSelected:null,
                toSearch:null,            
            }
        },
        methods: {
            save_contact(){
                if (this.new_contact.name && this.new_contact.email && this.new_contact.address && this.new_contact.phone && this.new_contact.country && this.new_contact.city){
                    //add the new_contact                                                           
                    this.contacts.push({...this.new_contact, id: this.get_nextContactId()});                                    
                    //reset the form                    
                    this.new_contact = {
                        id: null,
                        name:"",
                        email:"",
                        address:"",
                        phone:"",                   
                        name:"",
                        email:"",
                        address:"",
                        phone:"",
                        country:"",
                        city:""
                    }                                                   
                }
                else {
                    alert("Completa todos los campos")
                }

            },
            get_nextContactId(){               
               return this.contacts.length > 0 ? this.contacts[this.contacts.length -1].id+ 1 : 1;
               
            },
            get_contacts(){
                if(this.toSearch){
                    return this.contacts.filter(contact => contact.name.toLowerCase().includes(this.toSearch.toLowerCase()));
                }
                return this.contacts;
            },
            remove(id){
        
                if(confirm("Esta seguro de eliminar el contacto?"))
                {
                    let index = this.contacts.findIndex(contact => contact.id === id);
                    this.contacts.splice(index, 1);
                }
            },
            edit(id){
                let contact = this.contacts.find(contact => contact.id === id);
                if(contact !==-1> 0){
                    this.contactSelected = {...contact};
                }
                else{
                    console.error("contacto no encontrado");                   
                }
            },
            toggleModal(){ 
                //this.modal =!this.modal;
                this.contactSelected = null;

            },
            updateContact(updateContact){
                let index = this.contacts.findIndex(contact => contact.id === this.contactSelected.id);
                if(index !== -1){
                    this.contacts[index] =updateContact;                    
                }                
                this.toggleModal();
                const modal = bootstrap.Modal.getInstance(document.getElementById('editModal'))
                modal.hide();
            }

        },
        components: {
            Modal
        }

    }
</script>

<style>
    .btn {
        margin-right: 3px;
    }
    .card{
        overflow-x: auto;
    }
</style>