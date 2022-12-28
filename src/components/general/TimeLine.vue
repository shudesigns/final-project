<template>
    <div class="time-line">
        <div class="legends d-flex align-items-center">
            <div class="item-1 legend legend-1">康熙41年</div>
            <div class="item-2 legend legend-2">乾隆7年</div>
            <div class="item-3 legend legend-3">其他皇帝</div>
        </div>
        <div class="stacked-bar d-flex align-items-center">
            <template v-for="person in people" :key="person.key">
                <div class="line" v-if="person.dots"></div>
                <div class="bar" :class="person_active_state(person.key)"></div>
            </template>
        </div>
        <div class="legends d-flex align-items-center">
            <div class="item-1 legend legend-1">1681</div>
            <div class="item-2 legend legend-2">1742</div>
            <div class="item-3 legend legend-3">1820</div>
            <div class="item-4 legend legend-4">1861</div>
        </div>
        <div class="stories">
            <template v-for="person in people" :key="person.key">
                <Transition name="fade">
                    <div :class="`item-${person.key} story story-${person.key}`" v-if="person.story" v-show="person.key === active_person" v-html="person.story"></div>
                </Transition>
            </template>
        </div>
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
                return this.active_person === key ? `item-${key} bar-${key} active` : `item-${key} bar-${key} inactive`
            } else {
                return `item-${key} bar-${key}`
            }
        },
    }
}
</script>

<style lang="sass">
@import "/src/assets/sass/general/timeline"
</style>