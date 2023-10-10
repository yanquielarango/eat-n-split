<script setup>
import Button from './Button.vue'

defineProps({
    selectedFriend: {
        type: Object,
        
    },
    state: {
        type: Object,
        required: true,
    },
   
})

defineEmits(['selected-friend'])



//  const isSelected = selectedFriend?.id === friend.id

// console.log(selectedFriend)

</script>


<template>
   <ul v-for="friend in state" :key="friend.id">
        <li :class="selectedFriend?.id === friend.id ? 'selected' : ''">
            <img :src="friend.image" :alt="friend.name" />
            <h3>{{ friend.name }}</h3>

            <p v-if="friend.balance < 0" class="red"> {{ friend.name }} owes you  {{ Math.abs(friend.balance) }}</p>

            <p  v-else-if="friend.balance > 0"  class="green">You owe {{ friend.name }} {{ Math.abs(friend.balance) }}</p>

            <p v-else="friend.balance === 0">You and  {{ friend.name }} are even</p>

            <button class="button" @click="$emit('selected-friend', friend)">{{selectedFriend?.id === friend.id ? "Close" : "Select" }}  </button>
        </li>
   </ul> 
</template>