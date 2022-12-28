<template>

    <!-- header -->
    <header class="site-header">
        <div class="title">
            <h1 class="text-center mb-0">{{ title }}</h1>
        </div>
        <nav class="navbar d-block">
            <ul class="list-unstyled d-flex justify-content-center align-items-center gap-5 mb-0">
                <li v-for="area in areas" :key="area.key" :class="area_active_state(area.key)">
                    <button type="button" class="btn" @click="toggle_area(area.key)">
                        <span>{{ area.name }}</span>
                    </button>
                </li>
            </ul>
        </nav>
    </header>

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
                <template v-for="area in areas" :key="area.key">
                    <Transition name="fade">
                        <div class="map-area" v-if="area.image" v-show="area.key === active_area">
                            <img :src="require(`@/assets/images/${area.image}`)" class="d-block w-100" :alt="area.name" />
                        </div>
                    </Transition>
                </template>
                <template v-for="person in people" :key="person.dots">
                    <Transition name="fade">
                        <div class="map-dots" v-if="person.dots" v-show="show_dots(person.key)">
                            <img :src="require(`@/assets/images/${person.dots}`)" class="d-block w-100" :alt="person.name" />
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
import MapModal from './general/MapModal.vue'
import TimeLine from './general/TimeLine.vue'
export default {
    components: {
        MapModal, TimeLine
    },
    data() {
        return {
            title: '悠遊避暑山莊',
            active_area: '',
            areas: [
                {
                    key: 'all',
                    name: '顯示全部'
                },
                {
                    key: 1,
                    name: '宮廷區',
                    image: 'map-area-01.png'
                },
                {
                    key: 2,
                    name: '湖泊區',
                    image: 'map-area-02.png'
                },
                {
                    key: 3,
                    name: '平原區',
                    image: 'map-area-03.png'
                },
                {
                    key: 4,
                    name: '山岳寺廟區',
                    image: 'map-area-04.png'
                }
            ],
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
        toggle_area(key) {
            if (key !== 'all') {
                this.active_area = key
            } else {
                this.active_area = ''
            }
        },
        area_active_state(key) {
            if (this.active_area) {
                return this.active_area === key ? 'active' : 'inactive'
            } else {
                if (key === 'all') {
                    return 'active'
                } else {
                    return false
                }
            }
        },
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
@import "/src/assets/sass/general/_header.sass"
@import "/src/assets/sass/general/_sidebar"
@import "/src/assets/sass/general/_map"
</style>