<script setup>
import InputError from '@/Components/InputError.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import { useForm } from '@inertiajs/vue3';
import { ref } from 'vue';

const props = defineProps(['todo']);

const form = useForm({
    message: props.todo.message,
});

const editing = ref(false);
const showModal = ref(false);
const modalTitle = ref('');
const modalMessage = ref('');
const modalAction = ref(null);

const confirmAction = () => {
    modalAction.value();
    showModal.value = false;
};

const showConfirmModal = (title, message, action) => {
    modalTitle.value = title;
    modalMessage.value = message;
    modalAction.value = action;
    showModal.value = true;
};

const toggleStatus = () => {
    const newStatus = todo.status === 'doing' ? 'done' : 'doing';
    form.put(route('todos.update', todo.id), { data: { message: "edited", status: newStatus }, onSuccess: () => todo.status = newStatus });
};
</script>

<template>
    <div class="p-6 flex space-x-2">
        <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-gray-600 -scale-x-100" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
            <path stroke-linecap="round" stroke-linejoin="round" d="M8 12h.01M12 12h.01M16 12h.01M21 12c0 4.418-4.03 8-9 8a9.863 9.863 0 01-4.255-.949L3 20l1.395-3.72C3.512 15.042 3 13.574 3 12c0-4.418 4.03-8 9-8s9 3.582 9 8z" />
        </svg>
        <div class="flex-1">
            <div class="flex justify-between items-center">
                <div>
                    <span class="text-gray-800">{{ todo.user.name }}</span>
                    <small class="ml-2 text-sm text-gray-600">{{ new Date(todo.created_at).toLocaleString() }}</small>
                </div>
                <button class="block w-full px-4 py-2 text-left text-sm leading-5 text-gray-700 hover:bg-gray-100 focus:bg-gray-100 transition duration-150 ease-in-out" @click="() => { const newStatus = todo.status === 'doing' ? 'done' : 'doing'; form.put(route('todos.update', todo.id), { data: {status: newStatus }, onSuccess: () => todo.status = newStatus })}">
                    {{ todo.status.toUpperCase() }}
                </button>
                <button class="block w-full px-4 py-2 text-left text-sm leading-5 text-gray-700 hover:bg-gray-100 focus:bg-gray-100 transition duration-150 ease-in-out" @click="editing = true">
                    Edit
                </button>
                <button class="block w-full px-4 py-2 text-left text-sm leading-5 text-gray-700 hover:bg-gray-100 focus:bg-gray-100 transition duration-150 ease-in-out" @click="showConfirmModal('Delete Todo', 'Are you sure you want to delete this todo?', () => $inertia.delete(route('todos.destroy', todo.id)))">
                    Delete
                </button>
            </div>
            <form v-if="editing" @submit.prevent="form.put(route('todos.update', todo.id), { onSuccess: () => editing = false })">
                <textarea v-model="form.message" class="mt-4 w-full text-gray-900 border-gray-300 focus:border-indigo-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50 rounded-md shadow-sm"></textarea>
                <InputError :message="form.errors.message" class="mt-2" />
                <div class="space-x-2">
                    <PrimaryButton @click="showConfirmModal('Save Edit', 'Are you sure you want to save this edit?', () => form.put(route('todos.update', todo.id), { onSuccess: () => editing.value = false }))" class="mt-4">
                        Save
                    </PrimaryButton>
                    <button class="mt-4" @click="editing = false; form.reset(); form.clearErrors()">
                        Cancel
                    </button>
                </div>
            </form>
                <div v-if="showModal" class="fixed inset-0 flex items-center justify-center bg-gray-500 bg-opacity-75">
        <div class="bg-white p-6 rounded shadow-lg">
            <h2 class="text-xl font-bold mb-4">{{ modalTitle }}</h2>
            <p class="mb-6">{{ modalMessage }}</p>
            <div class="flex justify-end space-x-4">
                <button @click="showModal = false" class="bg-gray-200 px-4 py-2 rounded">Cancel</button>
                <button @click="confirmAction" class="bg-red-600 text-white px-4 py-2 rounded">Confirm</button>
            </div>
        </div>
    </div>
            <p v-else class="mt-4 text-lg text-gray-900">{{ todo.message }}</p>
        </div>
    </div>
</template>
