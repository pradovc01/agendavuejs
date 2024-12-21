<template>
        <div class="modal fade" id="editModal" tabindex="-1" aria-labelledby="editModalLabel" aria-hidden="true">

        <div class="modal-dialog modal-dialog-centered">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title" id="editModalLabel">Edit Contact</h5>
                    <button type="button" class="btn-close" @click="closeModal" data-bs-dismiss="modal" aria-label="Close">&times;</button>
                </div>   
                <form v-if="contactData" @submit.prevent="saveEdit()">
                    <div class="modal-body">
                       
                        <div class="mb-3">
                            <label for="name" class="form-label">Name</label>
                            <input type="text" id="name" v-model="contactData.name"  class="form-control"/>
                        </div>
                        <div class="mb-3">
                            <label for="email" class="form-label">Email</label>
                            <input type="text" id="email" v-model="contactData.email" class="form-control"/>
                        </div>
                        <div class="mb-3">
                            <label for="address" class="form-label">Address</label>
                            <input type="text" id="address" v-model="contactData.address"  class="form-control"/>
                        </div>
                        <div class="mb-3">
                            <label for="phone" class="form-label">Phone</label>
                            <input type="text" id="phone" v-model="contactData.phone"  class="form-control"/>
                        </div>
                        <div class="mb-3">
                            <label for="country" class="form-label">Country</label>
                            <input type="text" id="country" v-model="contactData.country"  class="form-control"/>
                        </div>
                        <div class="mb-3">
                            <label for="city" class="form-label">City</label>
                            <input type="text" id="city" v-model="contactData.city"  class="form-control"/>
                        </div>
                    </div>
                    <div class="modal-footer">
                            <button type="submit" class="btn btn-primary"> Save Changes </button>
                            <button type="button" class="btn btn-secondary" data-bs-dismiss="modal" @click="closeModal"> Cancel </button>
                    </div>
                    
                </form>             
            </div>
        </div>
        </div>
</template>

<script>
    export default{
        props: {
            contactData:{
                type: Object,
                required: true,
            }
        },
        methods: {
            closeModal() {
                this.$emit('close')
            },
            saveEdit() {
                this.$emit("save", this.contactData);
            }
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
