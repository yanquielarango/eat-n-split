<script setup>
import { computed, ref } from 'vue';
import Button from './Button.vue'

const props = defineProps({
    selectedFriend: {
        type: Object,
        required: true
    },
    handleSplitBill: {
        type: Function
    }
})

const bill = ref("")
const paidByUser = ref("")
const whoIsPaying = ref("user")

const paidByFriend = computed(() => {
    return  bill ? bill.value - paidByUser.value : ""
})

const handleSubmit = () => {
    if(!bill.value || !paidByUser.value) return
    handleSplitBill(whoIsPaying === 'user' ? paidByFriend : -paidByUser)

}

</script>



<template>
    <form class="form-split-bill" @submit.prevent="handleSubmit">
        <h2>Split a bill with {{ selectedFriend?.name }}</h2>

        <label>💰 Bill value</label>
        <input type="text"  v-model="bill"/>

        <label>🧍 Your expense</label>
        <input type="text" v-model="paidByUser" />

        <label>👫 {{ selectedFriend?.name }}'s expense</label>
        <input type="text"  disabled v-model="paidByFriend"/>

        <label>🤑 Who is playing the bill</label>
        <select v-model="whoIsPaying">
            <option value="user">You</option>
            <option value="friend">{{selectedFriend?.name }}</option>
        </select>

        <Button>Split bill</Button>
    </form>
</template>