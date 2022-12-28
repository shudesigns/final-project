<template>
    <!-- header -->
    <SiteHeader />

    <!-- main -->
    <main id="main" class="pb-5">
        <div class="container d-flex align-items-center">

            <!-- sidebar -->
            <div class="site-sidebar">
                <div
                    class="person"
                    v-for="person in people"
                    :key="person.key"
                    :class="person_active_state(person.key)"
                    @click="toggle_person(person.key)">
                    <div class="person-avatar">
                        <img :src="require(`@/assets/images/${person.avatar}`)" :alt="person.name" />
                    </div>
                    <div class="person-text">
                        <div class="icon" :style="{'background-color': person.icon}"></div>
                        <p class="text mb-0">{{ person.name }}</p>
                    </div>
                </div>
            </div>

            <!-- map -->
            <div class="map">
                <div class="map-base">
                    <img :src="require('@/assets/images/map-base.png')" class="w-100" alt="Map" />
                </div>
                <template v-for="person in people" :key="person.dots">
                    <Transition name="fade">
                        <div class="map-dots" v-if="person.dots" v-show="show_dots(person.key)">
                            <img :src="require(`@/assets/images/${person.dots}`)" class="w-100" :alt="person.name" />
                        </div>
                    </Transition>
                </template>
                <div class="map-dots">
                    <div class="dot" data-bs-toggle="modal" data-bs-target="#map_modal"></div>
                </div>
            </div>
        </div>

        <div class="container">
            <!-- timeline -->
            <TimeLine :active_person="active_person" :people="people" />
        </div>

    </main>

    <!-- map modal -->
    <MapModal />
</template>

<script>
import SiteHeader from './general/header/SiteHeader.vue'
import MapModal from './general/MapModal.vue'
import TimeLine from './general/TimeLine.vue'
export default {
    components: {
        SiteHeader, MapModal, TimeLine
    },
    data() {
        return {
            active_person: '',
            people: [
                {
                    key: 1,
                    name: '康熙皇帝',
                    avatar: 'p1.png',
                    icon: '#443307',
                    dots: 'map-dots-01.svg',
                    story: `<ul><li><div class="d-flex gap-2"><p class="mb-0">康熙 20 年(1681 年)，四月，康熙皇帝由喜峰口北上塞外巡視狩獵，設置木蘭圍場。</p><img src="${require('@/assets/images/p1-story-1.png')}" alt="" /></div></li><li class="mt-3"><div class="d-flex gap-2"><p class="mb-0">康熙 27 年(1688 年)，準噶爾之役始於準噶爾首領噶爾丹入侵喀爾喀蒙古，並乘勝進兵至內蒙古。</p><img src="${require('@/assets/images/p1-story-2.png')}" alt="" /></div></li></ul>`
                },
                {
                    key: 2,
                    name: '乾隆皇帝',
                    avatar: 'p2.png',
                    icon: '#74570d',
                    dots: 'map-dots-02.svg'
                },
                {
                    key: 3,
                    name: '其他皇帝',
                    avatar: 'p3.png',
                    icon: '#cf9d1d',
                    dots: 'map-dots-03.svg'
                },
                {
                    key: 'all',
                    name: '顯示全部',
                    avatar: 'p4.png',
                    icon: '#ffc74f'
                }
            ]
        }
    },
    methods: {
        person_active_state(key) {
            if (this.active_person) {
                return this.active_person === key ? 'active' : 'inactive'
            } else {
                return false
            }
        },
        toggle_person(key) {
            if (key !== 'all') {
                this.active_person = key
            } else {
                this.active_person = ''
            }
        },
        show_dots(key) {
            if (this.active_person) {
                return this.active_person === key 
            } else {
                return true
            }
        }
    }
}
</script>

<style lang="sass">
@import "/src/assets/sass/general/_sidebar"
@import "/src/assets/sass/general/_map"
</style>