<template>
    <Layout>
        <h1 class="text-3xl">Users</h1>
    </Layout>

    <Nav />

    <div style="margin-top: 600px">
        <p>The current time is {{ time }}</p>
        <Link
            href="/users"
            class="text-blue-500"
            preserve-scroll
        >
            Refresh
        </Link>
    </div>
</template>

<script>
import {Link} from "@inertiajs/inertia-vue3";
import Layout from "../Shared/Layout";

export default {
    name: 'Users',

    components: {
        Layout,
        Link,
    },

    props: {
        time: String,
    },
}
</script>
