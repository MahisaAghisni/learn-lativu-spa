<script setup>
import { onMounted, reactive } from "vue";
import * as Bootstrap from "bootstrap";
import { router, usePage } from "@inertiajs/vue3";
import Navbar from "../Components/Navbar.vue";
import Toast from "../Components/Toast.vue";

const state = reactive({
    toastRef: null,
    toastMessage: "",
});

const page = usePage();

router.on("finish", () => {
    state.toastMessage = page.props.toast.success;

    showToast();
});

onMounted(() => {
    state.toastRef = new Bootstrap.Toast("#app-toast", {
        autohide: true,
        delay: 3000,
    });
});

const showToast = () => state.toastRef.show();
</script>

<template>
    <Navbar />
    <main class="py-4">
        <slot />
    </main>
    <Toast id="app-toast" :message="state.toastMessage" />
</template>
