<template>
    <div>
        <h1>Admin (ruta protegida)</h1>
        <UButton @click="logout()" class="mt-4">Logout</UButton>
    </div>
</template>

<script setup lang="ts">
const { logout } = useFirebaseAuth();
</script>

<style scoped></style>