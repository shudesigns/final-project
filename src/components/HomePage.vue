<template>
    <SiteHeader />
    <main id="main">
        <div class="container d-flex">
            <SiteSidebar />
        </div>
    </main>
</template>

<script>
import SiteHeader from './general/header/SiteHeader.vue'
import SiteSidebar from './general/SiteSidebar.vue';

export default {
    components: {
        SiteHeader, SiteSidebar
    }
}
</script>