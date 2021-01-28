<template>
    <div>
        <div class="d-flex justify-content-between align-items-center mb-3">
            <h3 class="page-title">Contacts</h3>
            <button type="button" class="btn btn-success" @click.prevent="toggleModal">Add</button>
        </div>
        <div class="mb-5">
            <input type="email" class="form-control form-control-lg" v-model="search" placeholder="Search by name, email and company">
        </div>
        <ContactList :contacts="list" :handleEdit="handleEdit" :handleDelete="handleDelete"/>
        <ContactForm v-show="showModal" :form="form" :showModal="showModal" :toggleModal="toggleModal" :addContact="addContact" :editContact="editContact"/>
    </div>
</template>

<script>
    import ContactForm from '../components/ContactForm';
    import contacts from '../data/contactList'
    import ContactList from '../components/ContactList';

    const initialValue = {
        name: '',
        email: '',
        company: '',
        country: '',
        role: '',
    }
    export default {
        name: "Home",
        components: { ContactList, ContactForm},
        data() {
            return {
                showModal: false,
                contacts,
                search: '',
                form: {...initialValue}
            }
        },
        methods: {
            toggleModal() {
                this.showModal = !this.showModal
            },
            handleEdit(data){
                this.form = {...data}
                this.toggleModal()
            },
            addContact(data) {
                this.contacts.push(data)
                this.toggleModal()
            },
            editContact(data) {
                this.contacts = this.contacts.map(el => {
                    if (el.id === data.id){
                        el = data
                    }
                    return el
                })
                this.toggleModal()
            },
            handleDelete(id){
                const confirm = window.confirm("Are you sure ?");
                if (confirm){
                    this.contacts = this.contacts.filter(el => el.id !== id)
                }
            }
        }, computed: {
            list() {
                const str = this.search.toLowerCase()
                return this.contacts.filter(el => (el.name.toLowerCase().includes(str) || el.company.toLowerCase().includes(str) || el.email.toLowerCase().includes(str)))
            }
        },
        watch: {
            showModal() {
                if (!this.showModal){
                    this.form = initialValue
                }
            }
        }
    }
</script>

<style scoped>
    .page-title {
        margin: 0;
    }
</style>
