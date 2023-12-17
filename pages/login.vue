<script setup lang="ts">
import { account, ID } from '@/utils/appwrite'
import { storeToRefs } from 'pinia'
import { ref } from 'vue'
import { useAuthStore } from '~/store/auth.store'

useSeoMeta({
	title: 'Auth',
})

const store = useAuthStore()
const { isAuth } = storeToRefs(store)

// TODO: One object it will be better
const emailRef = ref('')
const passwordRef = ref('')
const nameRef = ref('')

const router = useRouter()

// TODO: Add validation
const login = async (email: string, password: string) => {
	await account.createEmailSession(email, password)
	const response = await account.get()
	if (response) {
		store.set({
			email: response.email,
			name: response.name,
			status: response.status,
		})

		emailRef.value = ''
		passwordRef.value = ''
		nameRef.value = ''

		router.push('/')
	}
}

const register = async () => {
	await account.create(
		ID.unique(),
		emailRef.value,
		passwordRef.value,
		nameRef.value
	)
	// login(emailRef.value, passwordRef.value)
}
</script>

<template>
	<div class="flex items-center justify-center min-h-screen">
		<div class="rounded bg-gray-800 w-1/4 p-5">
			<h1 class="text-2xl font-bold text-center mb-5">
				{{ isAuth ? `Logged in as ${isAuth}` : 'Not logged in' }}
			</h1>

			<form>
				<input placeholder="Email" v-model="emailRef" class="mb-3 text-black" />
				<input
					placeholder="Password"
					v-model="passwordRef"
					class="mb-3 text-black"
				/>
				<input placeholder="Name" v-model="nameRef" class="mb-3 text-black" />
				<div class="flex items-center justify-center gap-5">
					<button @click.prevent="login(emailRef, passwordRef)">Login</button>
					<button @click.prevent="register">Register</button>
				</div>
				<!-- <Button  @click="logout">Logout</Button> -->
			</form>
		</div>
	</div>
</template>
