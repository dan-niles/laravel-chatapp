<template>
    <div class="grid grid-cols-2">
        <div class="font-bold text-xl">{{currentRoom.name}} Chat</div>
        <div>
            <select
                v-model="selected"
                @change="$emit('roomchanged', selected)"
                class="float-right outline-none">
                <option 
                    v-for="(room, index) in rooms"
                    :key="index"
                    :value="room"
                >
                    {{room.name}}
                </option>
            </select>
        </div>
    </div>
</template>
<script>
export default {
    props: ['rooms', 'currentRoom'],
    data: function() {
        return {
            selected: this.currentRoom
        }
    },
    created() {
        this.seleted = this.currentRoom
    },
}
</script>
