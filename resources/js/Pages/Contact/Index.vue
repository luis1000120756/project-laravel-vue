<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head, Link } from '@inertiajs/vue3';

const props = defineProps({
    contacts: Array
})

console.log(props.contacts)
</script>

<template>

    <Head title="Contactos" />

    <AuthenticatedLayout>
        <template #header>

            <div class="flex justify-between">
                <h2 class="text-xl font-semibold leading-tight text-gray-800">
                    Contacts
                </h2>
                <Link :href="route('contacts.create')">
                Crear Contacto
                </Link>


            </div>

        </template>

        <div class="py-12">
            <div class="mx-auto max-w-7xl sm:px-6 lg:px-8">
                <div class="overflow-hidden bg-white shadow-sm sm:rounded-lg">
                    <table class="min-w-full divide-y divide-gray-200">
                        <thead class="bg-gray-100">
                            <tr>
                                <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase">Nombre</th>
                                <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase">Teléfono
                                </th>
                                <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase">Privacidad
                                </th>
                                <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase">Imágen</th>
                                <th class="px-6 py-3"></th>
                            </tr>
                        </thead>
                        <tbody class="bg-white divide-y divide-gray-200">
                            <tr v-for="contact in props.contacts" :key="contact.id">
                                <td class="px-6 py-4">{{ contact.name }}</td>
                                <td class="px-6 py-4">{{ contact.phone }}</td>
                                <td class="px-6 py-4 capitalize">{{ contact.privacity }}</td>
                                <img :src="`/project_vue_laravel/laravel-vue/public/storage/${contact.avatar}`"
                                    alt="Avatar" class="w-12 h-12 rounded-full object-cover" />




                                <td class="px-6 py-4 text-right">
                                    <!-- <Link :href="route('contacts.show', contact.id)" class="text-blue-600 hover:underline mr-3">Ver</Link>
                  <Link :href="route('contacts.edit', contact.id)" class="text-yellow-600 hover:underline">Editar</Link> -->
                                </td>
                            </tr>

                            <tr v-if="props.contacts.length === 0">
                                <td colspan="4" class="text-center py-4 text-gray-500">No hay contactos registrados.
                                </td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </div>
    </AuthenticatedLayout>
</template>
