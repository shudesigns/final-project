<template>
    <div class="site-sidebar">
        <div class="person" v-for="person in people" :key="person.name">
            <div class="person-avatar">
                <img :src="require(`@/assets/images/${person.avatar}`)" :alt="person.name" />
            </div>
            <div class="person-text">
                <div class="icon" :style="{'background-color': person.icon}"></div>
                <p class="text mb-0">{{ person.name }}</p>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            people: [
                {
                    name: '康熙皇帝',
                    avatar: 'p1.png',
                    icon: '#443307'
                },
                {
                    name: '乾隆皇帝',
                    avatar: 'p2.png',
                    icon: '#74570d'
                },
                {
                    name: '其他皇帝',
                    avatar: 'p3.png',
                    icon: '#cf9d1d'
                }
            ]
        }
    }
}
</script>

<style lang="sass">
@import "/src/assets/sass/general/_sidebar"
</style>