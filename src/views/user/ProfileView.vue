<script setup>
import UserLayout from '@/layouts/UserLayout.vue'
import { ref, onMounted } from 'vue';

const profileImageUrl = ref('https://img.daisyui.com/images/stock/photo-1534528741775-53994a69daeb.jpg')
const email = ref('')
const name = ref('')

onMounted(() => {
    let profileData = localStorage.getItem('profile-data')
    if (profileData) {
        profileData = JSON.stringify(profileData)
        profileImageUrl.value = profileData.imageUrl
        name.value = profileData.name
        email.value = profileData.email
    }
})

const handleFileUpload = (event) => {
    const file = event.target.files[0]

    if (file) {
        const reader = new FileReader()
        reader.onload = (e) => {
            profileImageUrl.value = e.target.result
        }
        reader.readAsDataURL(file)
    }
}  

const updateProfile = () =>  {
    const profileData = {
        imageUrl: profileImageUrl.value,
        name: name.value,
        email: email.value
    }
    localStorage.setItem('profile-data', JSON.stringify(profileData))
    alert('Update profile success')
}

</script>

<template>
    <UserLayout>
        <div class="max-w-xl mx-auto my-8 border border-base-200 shadow-xl">
            <div class="m-7">
                <div class="font-bold text-2xl">Your Profile</div>
                <div class="flex flex-col items-center">
                    <div>
                        <div class="avatar">
                            <div class="w-24 rounded-full">
                                <img :src="profileImageUrl">
                            </div>
                        </div>
                    </div>
                    <input type="file" @change="handleFileUpload"/>
                    <div class="form-control w-full max-w-xs">
                        <label class="label">
                          <span class="label-text">Email</span>
                        </label>
                        <input v-model="email" type="text" placeholder="Type here" class="input input-bordered w-full max-w-xs" />
                    </div>
                    <div class="form-control w-full max-w-xs">
                        <label class="label">
                          <span class="label-text">Name</span>
                        </label>
                        <input v-model="name" type="text" placeholder="Type here" class="input input-bordered w-full max-w-xs" />
                    </div>
                    <button @click="updateProfile" class="btn btn-neutral mt-6">Update Profile</button>
                </div>
            </div>
        </div>
    </UserLayout>
</template>