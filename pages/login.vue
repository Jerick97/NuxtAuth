<template>
    <div class="w-72 mx-auto">
        <h1 class="my-4 font-bold text-center text-2xl w-full">Login</h1>
        <UForm :schema="schema" :state="state" class="space-y-4" @submit="onSubmit">
            <UFormGroup label="Email" name="email" class="mb-4">
                <UInput v-model.trim="state.email" />
            </UFormGroup>

            <UFormGroup label="Password" name="password" class="mb-4">
                <UInput v-model.trim="state.password" type="password" />
            </UFormGroup>

            <UButton type="submit">
                Login
            </UButton>
        </UForm>
    </div>
</template>

<script setup lang="ts">
import { z } from 'zod'
import type { FormSubmitEvent } from '#ui/types'
const { login } = useFirebaseAuth();
const toast = useToast();
const schema = z.object({
    email: z.string().email('Invalid email'),
    password: z.string().min(8, 'Must be at least 8 characters')
})

type Schema = z.output<typeof schema>

const state = reactive({
    email: undefined,
    password: undefined
})

async function onSubmit(event: FormSubmitEvent<Schema>) {
    try {
        await login(event.data.email, event.data.password);
        toast.add({ title: 'Login successful', color: 'green', timeout: 2000, callback: async () => await navigateTo('/admin') });
    } catch (error) {
        console.error(error);
    }
}
</script>

<style scoped></style>