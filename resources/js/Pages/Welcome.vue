<script setup>
import { Head, Link } from '@inertiajs/vue3';
import SecondaryButton from '@/Components/SecondaryButton.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';

defineProps({
    canLogin: {
        type: Boolean,
    },
    canRegister: {
        type: Boolean,
    },
    laravelVersion: {
        type: String,
        required: true,
    },
    phpVersion: {
        type: String,
        required: true,
    },
});

function handleImageError() {
    document.getElementById('screenshot-container')?.classList.add('!hidden');
    document.getElementById('docs-card')?.classList.add('!row-span-1');
    document.getElementById('docs-card-content')?.classList.add('!flex-row');
    document.getElementById('background')?.classList.add('!hidden');
}
</script>

<template>
    <Head title="Welcome" />
<!--
        <img
            id="background"
            class="absolute -left-21 top-0 max-w-[877px]"
            src="https://laravel.com/assets/img/welcome/background.svg"
        />
-->
        <header class="grid grid-cols-2 items-center gap-2 py-10 lg:grid-cols-3">
            <nav v-if="canLogin" class="-mx-3 flex flex-1 justify-end">
            </nav>
        </header>
        <main class="mt-6 grid grid-cols-2">
            <aside class="content-center justify-self-center">
                <a href="/register"><PrimaryButton>Register</PrimaryButton></a>
                <a href="/login"><SecondaryButton>Login</SecondaryButton></a>
            </aside>
            <article class="space-y-10">
                <h1 class="text-black/100 text-2xl">Welcome to The Todo App&trade;!</h1>
                <p>The Todo App&trade; is a todo list app for listing down the stuff you have to do for the day.</p>
                <p>If you've ever faced with problems like....</p>
                <ul>
                    <li>Forgetting that feature until right after you finished drafting your GitHub Pull Request.</li>
                    <li>Missed an important phone call because you thought you had less stuff to do that day.</li>
                    <li>Overbooked too many tasks for yourself.</li>
                    <li>Forgot to bring home your dad after buying milk.</li>
                </ul>
                <p>...then this app is for you!</p>
                <p><a href="/register" class="text-green-600 hover:text-green-500">Sign up</a> now while it's FREE!</p>
                <p>PS: I made this in a way that requires authentication to manage a todo list. Different users have their own lists and can not be accessed by other users.</p>
            </article>
        </main>
        <footer class="py-16 text-center text-sm text-black dark:text-white/70">
        </footer>
</template>
