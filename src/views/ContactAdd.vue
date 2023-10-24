<template>
    <div class="page">
        <h4>Tạo liên hệ</h4>
        <ContactForm 
            :contact="contact" 
            @submit:contact="createContact"
        />
        <p>{{ message }}</p>
    </div>
</template>
<script>
import ContactForm from '../components/ContactForm.vue';
import contactService from '../services/contact.service';

export default {
    components: {
        ContactForm,
    },
    data() {
        return {
            contact: {},
            message: ""
        };
    },
    methods: {
        async createContact(data) {
            try {
                await contactService.create(data);
                this.message = "Liên hệ được tạo thành công.";
            } catch(error) {
                console.log(error);
            }
        }
    },
};
</script>