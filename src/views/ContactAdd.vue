<template>
    <div v-if="contact" class="page" style="max-width: 450px;">
        <h4>Thêm Liên hệ</h4>
        <ContactForm :contact="contact" @submit:contact="createContact" />
        <p>{{ message }}</p>
    </div>
</template>
<script>
import ContactForm from "@/components/ContactForm.vue";
import ContactService from "@/services/contact.service";

export default {
    components: {
        ContactForm,
    },

    data() {
        return {
            contact: {
                name: "",
                phone: "",
                email: "",
                address: "",
            },
            message: "",
        };
    },
    methods: {
        async createContact(data) {
            try {
                await ContactService.create(data);
                alert("Thêm liên hệ thành công.");
                this.$router.push({ name: "contactbook" });
            } catch (error) {
                console.log(error);
                this.message = "Có lỗi xảy ra khi thêm liên hệ.";
            }
        },
    },
};
</script>