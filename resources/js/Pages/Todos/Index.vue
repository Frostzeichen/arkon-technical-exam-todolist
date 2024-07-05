<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import Todo from '@/Components/Todo.vue';
import InputError from '@/Components/InputError.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import { useForm, Head } from '@inertiajs/vue3';

defineProps(['todos']);

const form = useForm({
    message: '',
    status: 'doing',
});
</script>

<template>
    <Head title="Todos" />

    <AuthenticatedLayout>
        <div class="max-w-2xl mx-auto p-4 sm:p-6 lg:p-8">
            <form @submit.prevent="form.post(route('todos.store'), { onSuccess: () => form.reset() })">
                <textarea
                    v-model="form.message"
                    placeholder="What would you like to do today?"
                    class="block w-full border-gray-300 focus:border-indigo-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50 rounded-md shadow-sm"
                ></textarea>
                <InputError :message="form.errors.message" class="mt-2" />
                <PrimaryButton class="mt-4">&rsaquo;</PrimaryButton>
            </form>

            <div class="mt-6 bg-white shadow-sm rounded-lg divide-y">
                <Todo
                    v-for="todo in todos"
                    :key="todo.id"
                    :todo="todo"
                />
            </div>
        </div>
    </AuthenticatedLayout>
</template>
