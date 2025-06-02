<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head, Link, useForm } from '@inertiajs/vue3';
import InputLabel from '@/Components/InputLabel.vue';
import TextInput from '@/Components/TextInput.vue';
import FileInput from '@/Components/FileInput.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import InputError from '@/Components/InputError.vue';

const form = useForm({
    name: "",
    phone: "",
    avatar: null,
    privacity: ""
});

const onSelectAvatar = (e) => {
    const files = e.target.files;
    if (files) {
        form.avatar = files[0];
    }
};

const submit = () => {
    form.post(route('contacts.store'))
    console.log('no recargo la pag');
}
</script>

<template>
    <Head title="Contactos" />

    <AuthenticatedLayout>
        <template #header>
            <div class="flex justify-between items-center">
                <h2 class="text-xl font-semibold leading-tight text-gray-800">Contacts</h2>
                <Link :href="route('contacts.create')" class="text-blue-600 hover:underline">
                    Crear Contacto
                </Link>
            </div>
        </template>

        <div class="py-12">
            <div class="max-w-md mx-auto bg-white shadow-md rounded-lg p-6">
                <form class="space-y-5" @submit.prevent="submit">
                    <div>
                        <InputLabel for="name" value="Nombre" />
                        <TextInput id="name" type="text" class="mt-1 block w-full" v-model="form.name" required autofocus />
                        <InputError class="mt-2" :message="form.errors.name" />
                    </div>

                    <div>
                        <InputLabel for="phone" value="Teléfono" />
                        <TextInput id="phone" type="text" class="mt-1 block w-full" v-model="form.phone" required />
                        <InputError class="mt-2" :message="form.errors.phone" />
                    </div>

                    <div>
                        <InputLabel for="avatar" value="Imagen" />
                        <FileInput name="avatar" @change="onSelectAvatar" />
                        <InputError class="mt-2" :message="form.errors.avatar" />
                    </div>

                    <div>
                        <InputLabel for="privacity" value="Privacidad" />
                        <select id="privacity" v-model="form.privacity"
                                class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:ring focus:ring-blue-200">
                            <option value="">Seleccionar...</option>
                            <option value="public">Público</option>
                            <option value="private">Privado</option>
                        </select>
                        <InputError class="mt-2" :message="form.errors.privacity" />
                    </div>

                    <div class="flex justify-end">
                        <PrimaryButton :disabled="form.processing">
                            Crear Contacto
                        </PrimaryButton>
                    </div>
                </form>
            </div>
        </div>
    </AuthenticatedLayout>
</template>
