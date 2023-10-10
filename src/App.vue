<script setup>
import {ref} from 'vue'
import FriendList from '@/components/FriendList.vue'
import {initialFriends} from '@/data.js'
import FormAddFriend from '@/components/FormAddFriend.vue'
import FormSplitBill from '@/components/FormSplitBill.vue'
import Button from '@/components/Button.vue'


const state = ref(initialFriends)
const showForm = ref(null)
const selectedFriend = ref()

const toggleForm = () => {
  showForm.value = !showForm.value
}

const createFriend = (friend) => {

  const id = crypto.randomUUID()

  state.value.push({
    id: id,
    name: friend.name,
    image: `${friend.image}?=${id}`,
    balance: 0
  })
}

const touchedFriend = (friend) => {
  // if(selectedFriend.id == friend.id) return selectedFriend.value = null
  selectedFriend.value = friend
  
}

const handleSplitBill = (value) => {
  console.log(value)
}


</script>



<template>
  <div class="app">
    <div class="sidebar">
      <FriendList :state="state" :selected-Friend="selectedFriend" @selected-friend="touchedFriend"/>
      
      <div v-show="showForm">
        <FormAddFriend :showForm="showForm" @create-friend="createFriend"/>
      </div>
      <Button @custom-toggle="toggleForm">{{ showForm ? 'Close' : 'Add friend' }}</Button>
          
    </div>

    <div v-show="selectedFriend">
      <FormSplitBill :selected-Friend="selectedFriend" :handleSplitBill="handleSplitBill"/>
    </div>
  </div>
</template>


