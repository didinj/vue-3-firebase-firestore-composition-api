<template>
  <div>
    <h2>Edit User</h2>
    <form @submit.prevent="updateUser">
      <input v-model="name" placeholder="Name" required />
      <input v-model="email" placeholder="Email" required type="email" />
      <button type="submit">Update</button>
      <button type="button" @click="deleteUser" style="margin-left: 1rem;">Delete</button>
    </form>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useRoute, useRouter } from 'vue-router';
import { db } from '../firebase';
import {
  doc,
  getDoc,
  updateDoc,
  deleteDoc
} from 'firebase/firestore';

const route = useRoute();
const router = useRouter();
const name = ref('');
const email = ref('');

const userRef = doc(db, 'users', route.params.id);

onMounted(async () => {
  const docSnap = await getDoc(userRef);
  if (docSnap.exists()) {
    const data = docSnap.data();
    name.value = data.name;
    email.value = data.email;
  }
});

const updateUser = async () => {
  await updateDoc(userRef, {
    name: name.value,
    email: email.value
  });
  router.push('/');
};

const deleteUser = async () => {
  await deleteDoc(userRef);
  router.push('/');
};
</script>
