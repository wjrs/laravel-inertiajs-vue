<template>
    <Head title="Users" />

    <div class="flex justify-between mb-6">
        <div class="flex items-center">
            <h1 class="text-3xl">Users</h1>

            <Link href="/users/create" class="text-blue-500 text-sm ml-2">New User</Link>
        </div>

        <input v-model="search" type="search" placeholder="Search..." class="border px-2 rounded-lg">
    </div>

    <div class="relative overflow-x-auto shadow-md sm:rounded-lg mt-6">
        <table class="w-full text-sm text-left text-gray-500 dark:text-gray-400">
            <thead class="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400">
            <tr>
                <th scope="col" class="px-6 py-3">
                    Name
                </th>
                <th scope="col" class="px-6 py-3">
                    <span class="sr-only">Edit</span>
                </th>
            </tr>
            </thead>
            <tbody>
            <tr
                v-for="user in users.data" :key="user.id"
                class="bg-white border-b dark:bg-gray-800 dark:border-gray-700"
            >
                <th scope="row" class="px-6 py-4 font-medium text-gray-900 dark:text-white whitespace-nowrap">
                    {{ user.name }}
                </th>
                <td class="px-6 py-4 text-right">
                    <Link
                        v-if="user.can.edit"
                        :href="`/users/${user.id}/edit`"
                        class="font-medium text-blue-600 dark:text-blue-500 hover:underline"
                    >
                        Edit
                    </Link>
                </td>
            </tr>
            </tbody>
        </table>
    </div>

    <Pagination
        :links="users.links"
        class="mt-6"
    />
</template>

<script>
import Pagination from "../../Shared/Pagination";
import {debounce} from "lodash";

export default {
    name: 'Users',

    components: {Pagination},

    data() {
        return {
            search: this.filters.search,
        }
    },

    props: {
        users: Object,
        filters: Object,
    },

    watch: {
        search: debounce(function (value) {
            this.searchFilter(value);
        }, 500)
    },

    methods: {
        searchFilter(value) {
            this.$inertia.get('/users', { search: value }, {
                preserveState: true,
                replace: true,
            })
        },
    }
}
</script>
