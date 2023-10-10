<script setup>
import { ref,  reactive } from 'vue';
import Button from './Button.vue'

defineProps({
    showForm : {
        type: Boolean,
    }
})

const friend = reactive({
    name: "",
    image: "https://i.pravatar.cc/48",
    balance: 0

})

const emit = defineEmits(['create-friend'])

const createFriend = () => {
    if(!friend.name || !friend.image) return
    emit('create-friend', friend)

    friend.name = ''
    friend.balance = 0
}

// defineEmits(['create-friend'])

</script>

<template>
   <div >
    <form class="form-add-friend"  @submit.prevent=" createFriend">
        <label>🧑‍🤝‍🧑 Friend name</label>
        <input type="text" v-model="friend.name" />

        <label>🌇 Image URL</label>
        <input type="text"  v-model="friend.image" />

        <Button>Add</Button>
     
    </form>
   </div>
</template>