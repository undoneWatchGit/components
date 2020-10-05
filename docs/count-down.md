# count-down

## Example:
```javascript
const endtime = 'Wed Sep 24 2020 17:00:00 GMT+0800'
<count-down :end-time="new Date(endtime)" >
 <template v-slot="{ hours, minutes, seconds }">

 </template>
</count-down>
```

## Slots

| Name      | Description                              |
| --------- | ---------------------------------------- |
| `default` | the slot provide hours, minutes, seconds |

## Props

| Name       | Type   | Description  |
| ---------- | ------ | ------------ |
| `end-time` | `Date` | endting time |

## Events

| Name    | Description                         |
| ------- | ----------------------------------- |
| `onend` | what happen when the count down end |

## Methods

### makeTimer()

**Syntax**

```typescript
makeTimer(): void
```

### onend()

**Syntax**

```typescript
onend(): void
```

