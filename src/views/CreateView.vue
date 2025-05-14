<template>
  <div class="q-pa-md" style="max-width: 300px">
    <q-form @submit="onSubmit" class="q-gutter-md">
      <q-input v-model="fname" label="First Name" />
      <q-input v-model="lname" label="Last Name" />
      <q-input v-model="username" label="Username" />
      <q-input v-model="password" label="Password" />
      <q-input v-model="email" label="Email" />
      <q-input v-model="avatar" label="Avatar" />
      <q-btn label="Submit" type="submit" color="primary" />
    </q-form>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router' 

const router = useRouter() 

const fname = ref('Cat')
const lname = ref('Chat')
const username = ref('cat.chat@melivecode.com')
const password = ref('1234')
const email = ref('cat.chat@melivecode.com')
const avatar = ref('https://www.melivecode.com/users/cat.png')

const onSubmit = () => {
  const raw = JSON.stringify({
    fname: fname.value,
    lname: lname.value,
    username: username.value,
    password: password.value,
    email: email.value,
    avatar: avatar.value
  })

  fetch("https://www.melivecode.com/api/users/create", {
    method: "POST",
    headers: {
      "Content-Type": "application/json"
    },
    body: raw
  })
    .then(res => res.json())
    .then(result => {
      console.log('📦', result)
      alert(result.message)
      if (result.status === 'ok') {
        router.push('/')
      }
    })
    .catch(err => {
      console.error('❌ Fetch error:', err)
      alert('เกิดข้อผิดพลาด: ' + err.message)
    })
}
</script>
