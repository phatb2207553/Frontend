<template> 
    <div v-if="contact" class="page"> 
        <h4>Tạo mới Liên hệ</h4> 
        <ContactForm :contact="contact" @submit:contact="createContact"/> 
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
    props: { 
    id: { type: String, required: true }, 
    },
    data() { 
        return { 
            contact: { name: "", email: "", address: "", phone: "", favorite: false }, //Khởi tạo liên hệ rỗng
            message: "", 
        }; 
    },
    methods: { 
        async createContact(data) { 
            try {
                await ContactService.create(data); 
                alert('Liên hệ được cập nhật thành công.'); 
                this.$router.push({ name: "contactbook" }); 
            } catch (error) { 
                console.log(error); 
            } 
        },
    }, 
    
    created() { 
        this.message = ""; 
    }, 
};
</script> 
