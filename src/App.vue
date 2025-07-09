<template>
  <div class="container">
    <nav>
      <router-link to="/">User List</router-link>
      <router-link to="/add">Add User</router-link>
    </nav>
    <router-view />
  </div>
</template>

<style>
.container {
  max-width: 600px;
  margin: 2rem auto;
  font-family: system-ui, sans-serif;
}

nav {
  display: flex;
  gap: 1rem;
  margin-bottom: 2rem;
}

nav a {
  text-decoration: none;
  color: #2c3e50;
  padding: 0.5rem 1rem;
  border: 1px solid #ccc;
  border-radius: 4px;
}

form {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

input {
  padding: 0.5rem;
  border: 1px solid #ccc;
  border-radius: 4px;
}

button {
  width: fit-content;
  padding: 0.5rem 1.5rem;
  background: #42b983;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
</style>
