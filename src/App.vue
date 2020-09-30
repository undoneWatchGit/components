<template>
  <Vote
    url="http://localhost:8080/api"
    slug="hello"
    voteFailMessage="hihihihi"
    @voted="onSuccess"
    @vote-faild="onFail"
  >
    <template v-slot="{ voteEvent, vote }">
      <div v-for="(item, index) in voteEvent.children" :key="index" @click="vote(item.productId)">
        {{ item.productId }}
      </div>
    </template>
  </Vote>
</template>
<script>
import Vote from './components/vote/index'
export default {
  components: {
    Vote
  },
  methods: {
    onFail(e) {
      console.log(e)
    },
    onSuccess(e) {
      console.log(e)
    }
  }
}
</script>