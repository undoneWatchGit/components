# index

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

| Name         | Description                                                       |
| ------------ | ----------------------------------------------------------------- |
| `vote-faild` | <br>**Arguments**<br><ul><li>**`voteFailMessage: any`**</li></ul> |
| `voted`      | <br>**Arguments**<br><ul><li>**`data: any`**</li></ul>            |

