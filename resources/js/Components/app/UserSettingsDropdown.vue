<script setup>
// Imports
import {Menu, MenuButton, MenuItems, MenuItem} from '@headlessui/vue'
import {ChevronDownIcon} from '@heroicons/vue/20/solid'
import ResponsiveNavLink from "@/Components/ResponsiveNavLink.vue";
import { useForm } from '@inertiajs/vue3';

// Uses

// Refs
const form = useForm({});

// Props & Emit

// Computed

// Methods
const logout = ()=>{
    const confirm = window.confirm('Are you sure to logout');
    if(!confirm) return;
    form.post(route('logout'))
    
}
// Hooks

</script>


<template>
    <Menu as="div" class="relative inline-block text-left">
        <div>
            <MenuButton
                class="inline-flex w-full justify-center rounded-md px-4 py-2 font-medium text-gray-800
                hover:bg-opacity-30 focus:outline-none focus-visible:ring-2 focus-visible:ring-white
                focus-visible:ring-opacity-75 capitalize"
            >
                {{ $page.props.auth.user.name }}

                <ChevronDownIcon
                    class="ml-2 -mr-1 h-5 w-5 text-gray-800"
                    aria-hidden="true"
                />
            </MenuButton>
        </div>

        <transition
            enter-active-class="transition duration-100 ease-out"
            enter-from-class="transform scale-95 opacity-0"
            enter-to-class="transform scale-100 opacity-100"
            leave-active-class="transition duration-75 ease-in"
            leave-from-class="transform scale-100 opacity-100"
            leave-to-class="transform scale-95 opacity-0"
        >
            <MenuItems
                class="absolute right-0 mt-2 w-32 origin-top-right divide-y divide-gray-100 rounded-md bg-white shadow-lg ring-1 ring-black ring-opacity-5 focus:outline-none"
            >
                <div class="px-1 py-1">
                    <MenuItem v-slot="{ active }">
                        <ResponsiveNavLink :href="route('profile')"
                                           :class="[active ? 'bg-gray-100 text-gray-900' : 'text-gray-700', 'block px-4 py-2']">
                            Profile
                        </ResponsiveNavLink>
                    </MenuItem>
                    <MenuItem v-slot="{ active }">
                        <ResponsiveNavLink @click="logout()" type="button" content="Logout" href="#"
                                           :class="[active ? 'bg-gray-100 text-gray-900' : 'text-gray-700', 'block px-4 py-2']">
                        </ResponsiveNavLink>
                    
                    </MenuItem>
                </div>
            </MenuItems>
        </transition>
    </Menu>
</template>


