<template>
    <div>
        <!-- the slot provide hours, minutes, seconds -->
        <slot :hours="hours" :minutes="minutes" :seconds="seconds"></slot>
    </div>
</template>
<script>
import dayjs from 'dayjs'
/**
 * example:
 * const endtime = 'Wed Sep 24 2020 17:00:00 GMT+0800'
 * <count-down end-time="new Date(endtime)" >
 *  <template v-slot="{ hours, minutes, seconds }">
 *    
 *  </template>
 * </count-down>
 */
export default {
    props: {
        /**
         * endting time
         */
        endTime: {
            type: Date
        }
    },
    data() {
        return {
            days: 0,
            hours: 0,
            minutes: 0,
            seconds: 0,
            timeUp: false,
            timer: null
        }
    },
    mounted() {
        this.timer = setInterval(() => {
            this.makeTimer()
        }, 1000)
    },
    beforeDestroy() {
        this.timer = null
    },
    methods: {
        makeTimer() {
            let timeLeft = dayjs(this.endTime).diff(dayjs(), 'second')
            if (timeLeft < 0) {
                this.onend()
                return
            }
            const hours = Math.floor(timeLeft / 3600)
            const minutes = Math.floor(
                (timeLeft - hours * 3600) / 60
            )
            const seconds = Math.floor(
                timeLeft - hours * 3600 - minutes * 60
            )

            const newTimer = {
                minutes,
                hours,
                seconds,
            }

            Object.assign(this.$data, newTimer)
        },
        onend() {
            clearInterval(this.timer)
            this.timeUp = true
            /**
                * what happen when the count down end
            */
            this.$emit('onend')
        }
    },
}
</script>
