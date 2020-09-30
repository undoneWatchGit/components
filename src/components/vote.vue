<template>
    <div>
        <slot :voteEvent="voteEvent" :vote="vote"/>
    </div>
</template>
<script>
import axios from 'axios'
/**
 * usage:
 * ```
 * <vote url="http://localhost:8080/api" slug="hello" >
 *   <template v-slot="{ voteEvent, vote }">
 *      <div v-for="(item, index) in voteEvent" :key="index" @click="vote">
 *         {{ item }}
 *      </div>
 *   </template>
 *  </vote>
 * ```
 * 
 */
export default {
    name: 'vote',
    props: {
        /**
         * the api url eg. http://localhost:8080/api
         */
        url: String,
        /**
         * the vote slug
         */
        slug: String,
        /**
         * default vote fail message
         */
        voteFailMessage: {
            type: String,
            default: 'voted before'
        }
    },
    data() {
        return {
            voteEvent: {}
        }
    },
    methods: {
        async fetchData() {
            const { data } = await axios.get(`${this.url}/vote/${this.slug}`)
            this.voteEvent = data
        },
        async vote(voteId) {
            if (localStorage.getItem(`vote-${this.slug}`)) {
                this.$emit('vote-faild', this.voteFailMessage)
                return
            }
            try {
                const { data } = await axios.post(`${this.url}/vote/${this.slug}/${voteId}`)
                this.$emit('voted', data)
                localStorage.setItem(`vote-${this.slug}`, true)
            } catch (error) {
                this.$emit('vote-faild', error)
            }
        }
    },
    mounted() {
        this.fetchData()
    }
}
</script>