<template class="contact">
    <div>
        <h1 class="contact">Hi its a Contact page</h1>
        <input type="email" v-model="email" placeholder="Email:">
        <input type="text" v-model="title" placeholder="Title">
        <textarea v-model="message"></textarea>
    </div>
<button type="submit" @click="submitForm" 
    href="mailto:manderson3600@gmail.com?cc=name2@rapidtables.com&bcc=name3@rapidtables.com
            &title=The%20subject%20of%20the%20email
            &message=The%20body%20of%20the%20email"
            >Send!</button>
</template>

<script>
export default {
    data() {
        return {
        email: '',
        title: '',
        message: ''
        }
    },
    methods: {
        submitForm(){
            this.email = '',
            this.title = '',
            this.message = ''
        }
    }
}
</script>

<style>
input, textarea {
    border: 5px solid rgb(138, 136, 136); 
    -webkit-box-shadow: 
      inset 0 0 8px  rgba(0,0,0,0.1),
            0 0 16px rgba(0,0,0,0.1); 
    -moz-box-shadow: 
      inset 0 0 8px  rgba(0,0,0,0.1),
            0 0 16px rgba(0,0,0,0.1); 
    box-shadow: 
      inset 0 0 8px  rgba(0,0,0,0.1),
            0 0 16px rgba(0,0,0,0.1); 
    padding: 15px;
    background: rgba(255,255,255,0.5);
    margin: 10px 30% 10px 30%;
}
.contact {
    display: block;
    
}
</style>