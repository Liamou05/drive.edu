<template>
    <nav class="min-w-[200px]">
        <Link :href="route('myFiles')" class="h-[80px] px-3 flex items-center gap-3 logo-link">
            <span class="logo-text">Drive<span class="logo-dot">.</span>edu</span>
        </Link>
        <div class="px-3">
            <CreateNewDropdown/>

            <div class="py-3">
                <NavLink :href="route('myFiles')" :active="$page.props.route_name === 'myFiles'">My Files</NavLink>
                <NavLink :href="route('file.sharedWithMe')" :active="$page.props.route_name === 'file.sharedWithMe'">Shared with me</NavLink>
                <NavLink :href="route('file.sharedByMe')" :active="$page.props.route_name === 'file.sharedByMe'">Shared by me</NavLink>
                <NavLink :href="route('trash')" :active="$page.props.route_name === 'trash'">Trash</NavLink>
            </div>
        </div>
    </nav>
</template>

<script setup>
// Imports
import {Link} from '@inertiajs/vue3'
import CreateNewDropdown from "@/Components/app/CreateNewDropdown.vue";
import NavLink from "@/Components/NavLink.vue";

// Uses

// Refs

// Props & Emit

// Computed

// Methods

// Hooks

</script>

<style scoped>
.logo-link {
    text-decoration: none;
}

.logo-text {
    font-size: 1.5rem;
    font-weight: 700;
    color: #1a1a1a;
    letter-spacing: -0.02em;
}

.logo-dot {
    color: #3b82f6;
}
</style>