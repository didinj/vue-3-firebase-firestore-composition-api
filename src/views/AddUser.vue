<template>
  <div>
    <h2>Add User</h2>
    <form @submit.prevent="addUser">
      <input v-model="name" placeholder="Name" required />
      <input v-model="email" placeholder="Email" required type="email" />
      <button type="submit">Add</button>
    </form>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { db } from '../firebase';
import { collection, addDoc } from 'firebase/firestore';
import { useRouter } from 'vue-router';

const name = ref('');
const email = ref('');
const router = useRouter();

const addUser = async () => {
  try {
    await addDoc(collection(db, 'users'), {
      name: name.value,
      email: email.value
    });
    router.push('/');
  } catch (error) {
    console.error("Error adding user:", error);
  }
};
</script>
