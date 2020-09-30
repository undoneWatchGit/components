<template>
    <div class="flex flex-col md:flex-row" ref="zoom">
        <div
            class="w-full md:w-1/2 overflow-hidden relative rounded-lg bg-gray-800 flex-shrink-0"
        >
            <slot name="reset" :reset="reset">
                <div
                    class="absolute z-10 top-0 right-0 p-4 text-white cursor-pointer"
                    @click="reset"
                >
                    <svg
                        width="18"
                        height="17"
                        viewBox="0 0 18 17"
                        class="fill-current text-white"
                    >
                        <path
                            d="M5.48 6.1L6.8 4.78 4.138 2.162 6.25.05H.75v5.5l2.112-2.112L5.48 6.1zm7.04 0l2.618-2.662L17.25 5.55V.05h-5.5l2.112 2.112L11.2 4.78l1.32 1.32zm4.73 10.45v-5.5l-2.112 2.112L12.52 10.5l-1.32 1.32 2.662 2.618-2.112 2.112h5.5zm-11 0l-2.112-2.112L6.8 11.82 5.48 10.5l-2.618 2.662L.75 11.05v5.5h5.5z"
                        ></path>
                    </svg>
                </div>
            </slot>
            <div
                class="w-full overflow-hidden zoom-image"
                :style="zoomImageStyle"
            ></div>
            <template v-if="isZooming">
                <slot name="overlay" />
            </template>
        </div>
        <div class="w-full md:w-1/2 md:px-4 py-4 flex overflow-scroll flex-shrink-0">
            <div class="flex flex-row md:flex-col md:justify-around w-full">
                <template v-for="(item, index) in texts">
                    <div
                        :key="index"
                        class="text zoom-text w-auto lg:w-full pr-2 flex-shrink-0 flex items-center"
                        :ref="`text-${index}`"
                        :class="activeitem == index ? 'active' : ''"
                        @click="onclick(item, index)"
                    >
                        <div class="cursor-pointer flex items-center md:items-start">
                            <slot name="pointer" :active="activeitem == index"></slot>
                            <div>
                                <div class="flex justify-start items-center">
                                    <div
                                        class="text-xl md:text-md lg:text-xl font-bold bold SctoGroteskA"
                                    >
                                        {{ item.title }}
                                    </div>
                                </div>
                                <div class="text-base md:text-sm lg:text-base hidden md:block">
                                    {{ item.content }}
                                </div>
                            </div>
                        </div>
                        <div class="w-8 md:hidden"></div>
                    </div>
                </template>
            </div>
        </div>
        <div class="SctoGroteskA">{{ activeContent }}</div>
    </div>
</template>
<script>
import { head, get } from 'lodash'
export default {
    name: 'zoom',
    props: {
        image: {
            type: String,
        },
        texts: {
            type: Array,
        },
        /**
         * this is for something
         */
        foo: {
            type: String
        }
    },
    data() {
        return {
            activeitem: 0,
            activeContent: get(head(this.texts), 'content'),
            position: {
                x: 0,
                y: 0,
                scale: 100,
            },
            isZooming: false
        }
    },
    watch: {
        activeitem() {
            this.$emit('update', this.activeitem)
        },
    },
    methods: {
        reset() {
            this.activeitem = 0
            this.zoomout()
            this.isZooming = false
        },
        zoomout() {
            this.position = { x: 0, y: 0, scale: 100 }
        },
        onclick(item, index) {
            this.zoomTo(item)
            this.activeitem = index
            this.activeContent = item.content
            this.isZooming = true
        },
        zoomTo(item) {
            this.position = {
                x: item.x,
                y: item.y,
                scale: item.scale ? item.scale : 150
            }
        },
    },
    computed: {
        zoomImageStyle() {
            return `background-image: url(${this.image});
                    background-position: ${50 + this.position.x}%  ${50 + this.position.y}%;
                    background-size: auto ${this.position.scale}%;
                    background-repeat: no-repeat;
                    transition:all 0.6s
                    `
        }
    }
}
</script>
<style lang="scss">
.zoom-text {
    opacity: 0.5;
}
.zoom-text.active {
    opacity: 1;
}
.zoom-image {
    height: 500px;
    @screen md {
        height: 750px;
    }
}
</style>
