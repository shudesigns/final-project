<template>
    <header class="site-header">
        <div class="title">
            <h1 class="text-center mb-0">{{ title }}</h1>
        </div>
        <nav class="navbar d-block">
            <ul class="list-unstyled d-flex justify-content-center align-items-center gap-5 mb-0">
                <li v-for="item in nav" :key="item.name">
                    <button type="button" class="btn">
                        <span>{{ item.name }}</span>
                    </button>
                </li>
            </ul>
        </nav>
    </header>
</template>

<script>
export default {
    data() {
        return {
            title: '悠遊避暑山莊',
            nav: [
                { name: '宮廷區' },
                { name: '湖泊' },
                { name: '平原' },
                { name: '山岳寺廟' }
            ]
        }
    }
}
</script>

<style lang="sass">
@import "/src/assets/sass/general/_header"
</style>