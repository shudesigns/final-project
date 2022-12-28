<template>
    <div class="time-line d-flex align-items-center">
        <template v-for="person in people" :key="person.key">
            <div class="line" v-if="person.dots"></div>
            <div class="bar" :class="person_active_state(person.key)"></div>
        </template>
    </div>
</template>

<script>
export default {
    props: {
        active_person: {
            require: true
        },
        people: {
            require: true
        }
    },
    methods: {
        person_active_state(key) {
            if (this.active_person) {
                return this.active_person === key ? 'bar-' + key + ' active' : 'bar-' + key + ' inactive'
            } else {
                return 'bar-' + key
            }
        },
    }
}
</script>

<style lang="sass">
@import "/src/assets/sass/general/timeline"
</style>