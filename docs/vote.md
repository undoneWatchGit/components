# vote

usage:
```
<vote url="http://localhost:8080/api" slug="hello" >
<template v-slot="{ voteEvent, vote }">
<div v-for="(item, index) in voteEvent" :key="index" @click="vote">
{{ item }}
</div>
</template>
</vote>
```

## Slots

| Name      | Description |
| --------- | ----------- |
| `default` | &nbsp;      |

## Props

| Name                | Type     | Description                               | Default          |
| ------------------- | -------- | ----------------------------------------- | ---------------- |
| `url`               | `String` | the api url eg. http://localhost:8080/api |                  |
| `slug`              | `String` | the vote slug                             |                  |
| `vote-fail-message` | `String` | default vote fail message                 | `"voted before"` |

## Events

| Name         | Description                                                                              |
| ------------ | ---------------------------------------------------------------------------------------- |
| `fetch`      | send out the data after fetch<br>**Arguments**<br><ul><li>**`voteEvent: any`**</li></ul> |
| `vote-faild` | <br>**Arguments**<br><ul><li>**`voteFailMessage: any`**</li></ul>                        |
| `voted`      | <br>**Arguments**<br><ul><li>**`data: any`**</li></ul>                                   |

## Methods

### fetchData()

**Syntax**

```typescript
async fetchData(): Promise
```

### vote()

**Syntax**

```typescript
async vote(voteId: unknow): Promise
```

