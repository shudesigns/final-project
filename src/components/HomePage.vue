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
                        <div
                            :class="`map-area area-${area.key} ${area.key === active_area ? 'active' : ''}`"
                            v-if="area.image"
                            v-show="area.key === active_area">
                            <div class="area-image">
                                <div class="toggle" @mouseenter="area.show_desc = true" @mouseleave="area.show_desc = false"></div>
                                <img :src="require(`@/assets/images/${area.image}`)" class="d-block w-100" :alt="area.name" />
                            </div>
                            <Transition name="fade">
                                <div class="area-description" v-if="area.show_desc" v-html="area.description"></div>
                            </Transition>
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
                    name: '首頁'
                },
                {
                    key: 1,
                    name: '宮廷區',
                    image: 'map-area-01.png',
                    description: `<h5>宮殿區：移動的紫禁城</h5><p class="mb-0">避暑山莊宮殿區位於山莊南部，是清朝皇帝駐蹕山莊時處理朝政、舉行慶典與寢居空間。由正宮、東宮、萬壑松風與松鶴齋四部分組成。正宮建築規格依循北京紫禁城中軸線前朝後寢布局興建，具有對稱、規整與莊嚴特點。前朝以澹泊敬誠殿，後寢則以煙波致爽殿為代表。清代中晚期，嘉慶與咸豐兩位皇帝先後在山莊駕崩，國勢也開始慢慢進入夕陽黃昏。</p>`,
                    show_desc: false
                },
                {
                    key: 2,
                    name: '湖泊區',
                    image: 'map-area-02.png',
                    description: `<h5>湖泊區：文化與物資的匯聚</h5><p class="mb-0">山莊湖泊區緊鄰於宮殿區，由九個大小湖泊組成，湖內島嶼林立，各有名稱，如文園島、如意洲、青蓮島、金山、月色江聲島等。島湖小橋長堤相連，樓閣亭榭，綠樹成蔭，不僅部分植物盆栽移植自帝國內地，區內建築也有模仿自江南園林布局，例如青蓮島的煙雨樓是據浙江嘉興煙雨樓而建，文園獅子林則仿自蘇州獅子林，金山島設計是來自鎮江金山，一派江南水鄉風光，因此有「塞外江南」之稱。湖泊區是清代帝后駐蹕山莊時避暑休憩去處，康熙、乾隆兩帝更為山莊各取三十六美景，留下許多官方刊物與圖繪。</p>`,
                    show_desc: false
                },
                {
                    key: 3,
                    name: '平原區',
                    image: 'map-area-03.png',
                    description: `<h5>平原區：外交場域</h5><p class="mb-0">平原區位於避暑山莊東北部，區內分東西兩部，西部草地以「試馬埭」為主體，是清帝與蒙古王公圍獵前試馬選馬的場地；東部林地則以「萬樹園」為代表，園區佈滿大大小小蒙古包，呈現北方蒙古草原景色。康熙年間萬樹園作為山莊行獵之處，而到了乾隆時期進行大規模擴建，賦予了此區在聯結外藩蒙藏王公貴族、宗教領袖以及國外使節外交朝覲筵宴的重要功能。</p>`,
                    show_desc: false
                },
                {
                    key: 4,
                    name: '寺廟山嶽區',
                    image: 'map-area-04.png',
                    description: `<h5>寺廟山嶽區：信仰與政治</h5><p class="mb-0">環繞山莊周邊外圍，自北至東南，沿獅子溝至武烈河東岸丘陵山巒區，漢藏式的寺廟林立，其中以北京理藩院統一管理的古北口外八座寺廟，俗稱的「外八廟」最為著名，是清帝國為紀念重要大事時特地興建的寺廟。例如為康熙五十二年(1713)紀念蒙古王公首次前來山莊覲見並為康熙皇帝祝壽而建的溥仁寺與溥善寺；乾隆二十年代初期為慶祝平定準噶爾蒙古而建的普寧寺、乾隆二、三十年代間為紀念蒙古民族歸附覲見先後營建的安遠廟、普樂寺、普陀宗乘之廟，以及乾隆四十五年(1780)為迎接西藏六世班禪來華並向乾隆皇帝祝壽所興建的須彌福壽之廟等。清帝國透過宗教信仰，藉以鞏固並加強與信奉藏傳佛教蒙藏民族的關係，從而達到北疆國防長治久安的一種政治策略。</p>`,
                    show_desc: false
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