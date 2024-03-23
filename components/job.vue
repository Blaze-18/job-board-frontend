<script setup>
import { useUserStore } from '@/stores/user'

const userStore = useUserStore()

const emit = defineEmits(['deleteJob'])

const props = defineProps({
    my: {
        type: [Boolean]
    },
    job: {
        type: [Object]
    }
})

async function deleteJob(id) {
    await $fetch('https://blazeforyou.pythonanywhere.com/api/v1/jobs/' + id + '/delete/', {
        method: 'DELETE',
        headers: {
            'Authorization': 'token ' + userStore.user.token,
            'Content-Type': 'application/json'
        },
    })
    .then(response => {
        console.log('response', response)

        emit('deleteJob', id)
    })
    .catch(error => {
        console.log(error)
    })
}
</script>

<template>
    <div class="p-6 flex items-center justify-between bg-gray-100 rounded-xl">
        <div>
            <h3 class=" mb-2 text-xl font-semibold ">{{ job.title }}</h3>
            <p class=" text-gray-600 font-medium">{{ job.company_name }}</p>
        </div>

        <div>
            <p class="mb-2 font-bold">{{ job.position_location }}</p>
            <p>{{ job.position_salary }}</p>
        </div>

        <div>
            <p>Posted at {{ job.created_at_formatted }} </p>
        </div>


        <div class="space-x-4">
            <NuxtLink v-bind:to="'/browse/'+job.id" class=" py-4 px-6 bg-teal-700 hover:bg-green-600 rounded-xl text-white" style="font: bold;">Details
            </NuxtLink>
            <NuxtLink v-bind:to="'/editjob/'+job.id" class=" py-4 px-6 bg-cyan-700 hover:bg-green-600 rounded-xl text-white" v-if="my" style="font: bold;">Edit
            </NuxtLink>
            <a @click="deleteJob(job.id)" class=" py-4 px-6 bg-rose-700 hover:bg-green-600 rounded-xl text-white" v-if="my" style="font: bold;">Delete
            </a>
        </div>


    </div>
</template>