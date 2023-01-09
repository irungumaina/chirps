<script setup>
import AppLayout from '@/Layouts/AppLayout.vue';
import Chirp from '@/Components/Chirp.vue';
import InputError from '@/Components/InputError.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import { useForm, Head } from '@inertiajs/inertia-vue3';
// import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';


defineProps(['chirps']);

const form = useForm({
    message: '',
});
</script>

<template>
    <AppLayout title="Chirps">
        <template #header>
            <h2 class="text-xl font-semibold leading-tight text-gray-800">
                Chirps
            </h2>
        </template>

        <div class="py-12">
            <div class="mx-auto max-w-7xl sm:px-6 lg:px-8">
                <div class="overflow-hidden bg-white shadow-xl sm:rounded-lg">
                    <div class="max-w-2xl p-4 mx-auto sm:p-6 lg:p-8">
                        <form @submit.prevent="form.post(route('chirps.store'), { onSuccess: () => form.reset() })">
                            <textarea
                                v-model="form.message"
                                placeholder="What's on your mind?"
                                class="block w-full border-gray-300 rounded-md shadow-sm focus:border-indigo-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50"
                            ></textarea>
                            <InputError :message="form.errors.message" class="mt-2" />
                            <PrimaryButton class="mt-4">Chirp</PrimaryButton>
                        </form>

                        <div class="mt-6 bg-white shadow-sm rounded-lg divide-y">
                            <Chirp
                            v-for="chirp in chirps"
                            :key="chirp.id"
                            :chirp="chirp"
                            />
                        </div>


                    </div>
                </div>
            </div>
        </div>
    </AppLayout>
</template>
