<template>
    <div class="relative h-10 m-4">
        <div style="border-top: 0px solid #e6e6e6" class="grid grid-cols-6">
            <input 
                type="text" 
                v-model="message"
                @keyup.enter="sendMessage()"
                placeholder="Say something..."
                class="col-span-5 outline-none p-1 rounded-lg"
                style="border: 1px solid #e6e6e6"
            />
            <button
                @click="sendMessage()"
                class="align-middle place-self-start bg-gray-500 hover:bg-blue-700 p-2 mx-1 rounded-lg text-white outline-none">
                Send
            </button>
        </div>
    </div>
</template>
<script>
export default {
    props: ['room'],
    data: function() {
        return {
            message: ''
        }
    },
    methods: {
        sendMessage() {
            if(this.message == '') {
                return;
            }
            axios.post('/chat/room/' + this.room.id + '/message', {
                message: this.message
            })
            .then(response => {
                if(response.status == 201) {
                    this.message = '';
                    this.$emit('messagesent');
                }
            })
            .catch(error => {
                    console.log(error);
            })
        },
    },
}
</script>
