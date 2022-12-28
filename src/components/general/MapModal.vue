<template>
    <div class="modal fade modal-lg" id="map_modal" tabindex="-1">
        <div class="modal-dialog modal-dialog-centered modal-dialog-scrollable">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title">
                        {{ modal.title }}
                    </h5>
                    <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                </div>
                <div class="modal-body">
                    <div class="row row-cols-2">
                        <div class="col">
                            <img :src="require(`@/assets/images/${modal.image.src}`)" :alt="modal.image.alt" class="w-100" />
                        </div>
                        <div class="col d-flex flex-column">
                            <template v-for="(page, index) in modal.pages" :key="page.content">
                                <div
                                    class="content flex-grow-1"
                                    v-html="page.content"
                                    v-if="this.modal.display_page === index">
                                </div>
                            </template>
                            <div class="buttons flex-shrink-0 d-flex justify-content-end align-items-center gap-1">
                                <button
                                    v-for="button in modal.buttons"
                                    :key="button.dir"
                                    type="button"
                                    class="btn"
                                    :class="button_class(button.dir)"
                                    @click="button_click(button.dir)">
                                    <i :class="button.icon"></i>
                                </button>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            modal: {
                title: '冷枚避暑山莊圖軸',
                display_page: 0,
                image: {
                    src: 'modal-image.png',
                    alt: '冷枚避暑山莊圖軸',
                },
                pages: [
                    {
                        content: `<small>《避暑山莊圖》軸，清，冷枚作，絹本，設色，縱254.8厘米，橫172.5厘米。</small><p class="mt-3" style="line-height: 1.75">作者以寫實的手法描繪了避暑山莊後苑部分及其四周的崇山峻嶺。構圖為鳥瞰式，自景區上方向下縱向取景，景緻具體而微。設色以青綠著色和淺絳渲染相結合，冷暖色調和諧呼應，成功地營造出山莊靜寂清幽的氛圍。筆法靈活多變，山石樹木或以乾筆皴擦，或青綠烘染。建築物的描繪，作者在傳統的工筆界畫基礎上，又巧妙地吸收了歐洲的透視法，並將二者融合在一起，從而更科學、客觀地表現出建築物的物理結構，同時也加強了畫面的縱深感。此圖同時是一幅反映康熙時期避暑山莊建築的圖樣，對於我們了解避暑山莊的建築沿革有著重要的圖像價值。</p>`,
                    },
                    {
                        content: `<h6 class="fw-bold">對應現代地圖</h6><img src="${require('@/assets/images/modal-gmap.png')}" class="w-100" alt="現代地圖" />`
                    }
                ],
                buttons: [
                    { icon: 'bi-chevron-left', dir: 'prev' },
                    { icon: 'bi-chevron-right', dir: 'next' }
                ]
            }
        }
    },
    methods: {
        button_class(dir) {
            if (dir === 'prev' && this.modal.display_page === 0) {
                return 'disabled'
            } else if (dir === 'next' && this.modal.display_page === this.modal.pages.length - 1) {
                return 'disabled'
            } else {
                return ''
            }
        },
        button_click(dir) {
            if (dir === 'prev' && this.modal.display_page !== 0) {
                this.modal.display_page--
            }
            else if (dir === 'next' && this.modal.display_page !== this.modal.display_page.length - 1) {
                this.modal.display_page++
            }
        }
    },
    mounted() {
        const app = this
        const modal_el = document.getElementById('map_modal')
        modal_el.addEventListener('hidden.bs.modal', () => {
            app.modal.display_page = 0
        })
    }
}
</script>

<style lang="sass">
@import "/src/assets/sass/general/_modal"
</style>