<template>
    <div class="modal-overlay active" >
        <div class="modal is-open" tabindex="-1">
            <div class="modal-dialog">
                <div class="modal-content">
                    <form @submit.prevent="handleSubmit">
                        <div class="modal-header">
                            <h5 class="modal-title">{{form.id ? 'Edit' : 'Create'}} Contact</h5>
                            <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close" @click="this.toggleModal"></button>
                        </div>
                        <div class="modal-body">

                            <div class="row mb-3">
                                <label for="name" class="col-sm-2 col-form-label">Name</label>
                                <div class="col-sm-10">
                                    <input type="text" v-model="form.name" class="form-control" :class="($v.form.name.$dirty && !$v.form.name.required) && 'is-invalid'" id="name"
                                           placeholder="Contact Name">
                                    <div  class="invalid-feedback" v-show="$v.form.name.$dirty && !$v.form.name.required">
                                        Please enter name.
                                    </div>
                                </div>
                            </div>
                            <div class="row mb-3">
                                <label for="email" class="col-sm-2 col-form-label">Email</label>
                                <div class="col-sm-10">
                                    <input type="email" v-model="form.email" class="form-control" :class="(($v.form.email.$dirty && !$v.form.email.required) || ($v.form.email.$dirty && !$v.form.email.email)) && 'is-invalid'" id="email"
                                           placeholder="Contact Email">
                                    <div  class="invalid-feedback" v-show="($v.form.email.$dirty && !$v.form.email.required) || ($v.form.email.$dirty && !$v.form.email.email)">
                                        Please enter valid email.
                                    </div>
                                </div>
                            </div>
                            <div class="row mb-3">
                                <label for="company" class="col-sm-2 col-form-label">Company</label>
                                <div class="col-sm-10">
                                    <input type="text" v-model="form.company" class="form-control" id="company"
                                           placeholder="Contact Company" :class="($v.form.company.$dirty && !$v.form.company.required) && 'is-invalid'">
                                    <div  class="invalid-feedback" v-show="$v.form.company.$dirty && !$v.form.company.required">
                                        Please enter company.
                                    </div>
                                </div>
                            </div>
                            <div class="row mb-3">
                                <label for="country" class="col-sm-2 col-form-label">Country</label>
                                <div class="col-sm-10">
                                    <multiselect id="country" v-model="form.country" :options="countries"
                                                 :searchable="false"
                                                 :show-labels="false"
                                                 :class="($v.form.country.$dirty && !$v.form.country.required) && 'is-invalid'"
                                                 placeholder="Contact Company"></multiselect>
                                    <div  class="invalid-feedback" v-show="$v.form.country.$dirty && !$v.form.country.required">
                                        Please select country.
                                    </div>
                                </div>
                            </div>
                            <div class="row mb-3">
                                <label for="role" class="col-sm-2 col-form-label">Role</label>
                                <div class="col-sm-10">
                                    <multiselect id="role" v-model="form.role" :options="roles" :searchable="false"
                                                 :show-labels="false"
                                                 :class="($v.form.role.$dirty && !$v.form.role.required) && 'is-invalid'"

                                                 placeholder="Contact Role"></multiselect>
                                    <div  class="invalid-feedback" v-show="$v.form.role.$dirty && !$v.form.role.required">
                                        Please select role.
                                    </div>
                                </div>
                            </div>

                        </div>
                        <div class="modal-footer">
                            <button type="button" class="btn btn-secondary" @click="this.toggleModal">Cancel</button>
                            <button type="submit" class="btn btn-success">{{form.id ? 'Edit' : 'Create'}}</button>
                        </div>
                    </form>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import {required, email} from 'vuelidate/lib/validators'
    import Multiselect from 'vue-multiselect'
    import countries from '../data/countryList'
    import roles from '../data/roleList'
    import {generateId} from '../helpers/generateId';

    export default {
        name: "ContactForm",
        props: {
            form: Object,
            showModal: Boolean,
            toggleModal: Function,
            editContact:Function,
            addContact:Function
        },
        data() {
            return {
                countries,
                roles,
            }
        },
        validations: {
            form: {
                name: {required},
                email: {required, email},
                company: {required},
                country: {required},
                role: {required},
            }
        },
        components: {
            Multiselect
        },
        methods: {
            handleSubmit() {
                this.$v.$touch()
                if (this.$v.$invalid){
                    return
                }else{
                    if (this.form.id){
                        this.editContact({...this.form})

                    }else{
                        this.addContact({id: generateId(5),...this.form})
                    }
                }
                this.$v.$reset()
            }
        }
    }
</script>

<style scoped>
    @import "~vue-multiselect/dist/vue-multiselect.min.css";

    .col-form-label {
        text-align: left;
    }

    input::placeholder {
        color: #adadad;
        font-size: 14px;
        opacity: 1;
    }

    input:-ms-input-placeholder {
        color: #adadad;
        font-size: 14px
    }

    input::-ms-input-placeholder {
        color: #adadad;
        font-size: 14px
    }

    .is-open {
        display: block;
    }

    .modal-overlay {
        display: none;
    }

    .modal-overlay.active {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100vh;
        background: rgba(0, 0, 0, 0.35);
        display: block;
    }

</style>
