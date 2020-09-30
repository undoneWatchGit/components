# zoom

## Slots

| Name      | Description |
| --------- | ----------- |
| `reset`   |             |
| `overlay` |             |
| `pointer` | &nbsp;      |

## Props

| Name    | Type     | Description           |
| ------- | -------- | --------------------- |
| `image` | `String` |                       |
| `texts` | `Array`  |                       |
| `foo`   | `String` | this is for something |

## Methods

### reset()

**Syntax**

```typescript
reset(): void
```

### zoomout()

**Syntax**

```typescript
zoomout(): void
```

### onclick()

**Syntax**

```typescript
onclick(item: unknow, index: unknow): void
```

### zoomTo()

**Syntax**

```typescript
zoomTo(item: unknow): void
```

 |                  |
| `vote-fail-message` | `String` | default vote fail message                 | `"voted before"` |

## Events

| Name         | Description                                                       |
| ------------ | ----------------------------------------------------------------- |
| `vote-faild` | <br>**Arguments**<br><ul><li>**`voteFailMessage: any`**</li></ul> |
| `voted`      | <br>**Arguments**<br><ul><li>**`data: any`**</li></ul>            |

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

