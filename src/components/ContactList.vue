<template>
    <div class="contact-accordion">
        <p class="result mb-5">Found {{contacts.length}} contacts</p>
        <div class="contact-accordion-item mb-3" :class="activeItem === contact.id ? 'is-open': ''"
             v-for="(contact,index) in contacts" :key="index" ref="items">
            <div class="contact-accordion-title" @click="toggleAccordion(contact.id)">
                <div class="title-text">
                    <div class="title-top">
                        <img src="../assets/arrow-down.svg" alt="arrow-down" class="arrow">
                        <h5>{{contact.name}}</h5>
                    </div>

                    <div class="title-bottom">
                        <span>{{contact.role}} at {{contact.company}}</span>
                    </div>
                </div>

                <div class="contact-accordion-action">
                    <img src="../assets/edit.svg" alt="edit" class="mr-2" @click.stop="handleEdit(contact)">
                    <img src="../assets/trash.svg" alt="delete" @click.stop="handleDelete(contact.id)">
                </div>
            </div>

            <div class="contact-accordion-body">
                <p>email - {{contact.email}}</p>
                <p>from - {{contact.country}}</p>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: "ContactList",
        props: {
            contacts: {
                type: Array,
                required: true,
            },
            handleEdit: Function,
            handleDelete:Function
        },
        data() {
            return {
                activeItem: null
            }
        },
        methods: {
            toggleAccordion(id) {
                this.activeItem = this.activeItem === id ? null : id
            }

        }
    }
</script>

<style scoped>
    .contact-accordion-item {
        border: 1px solid #dfdfdf;
        text-align: left;
        padding: 7px 15px;

    }

    .contact-accordion-title {
        display: flex;
        justify-content: space-between;
    }

    .contact-accordion-body {
        padding-top: 15px;
        height: 0;
        overflow: hidden;
        transition: height ease .5s;
    }

    .is-open .contact-accordion-body {
        height: 100px;
        transition: height ease .5s;
    }

    .arrow {
        display: block;
        width: 15px;
        margin-right: 10px;
        transform: rotate(-90deg);
        transition: transform ease .3s;
    }

    .is-open .arrow {
        transform: rotate(0deg);
        transition: transform ease .3s;
    }

    .title-top {
        display: flex;
        align-items: center;
        margin-bottom: 10px;
    }

    .title-top h5 {
        margin-bottom: 0;
    }

    .title-bottom, .result {
        color: #adadad;
    }

    .contact-accordion-action {
        max-width: max-content;
        width: 100%;
        display: flex;
    }

    .contact-accordion-action img {
        width: 15px;
        display: block;
        cursor: pointer;
    }
</style>
