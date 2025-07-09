<template>
  <div>
    <h2>User List</h2>
    <ul>
      <li v-for="user in users" :key="user.id">
        {{ user.name }} ({{ user.email }})
        <router-link :to="`/edit/${user.id}`">Edit</router-link>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { db } from '../firebase';
import { collection, onSnapshot } from 'firebase/firestore';

const users = ref([]);

onMounted(() => {
  const unsub = onSnapshot(collection(db, 'users'), (snapshot) => {
    users.value = snapshot.docs.map(doc => ({
      id: doc.id,
      ...doc.data()
    }));
  });
});
</script>
