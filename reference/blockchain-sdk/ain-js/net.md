# ain.net

## isListening

```text
ain.net.isListening()
```

### Returns

`Promise` returns a `Boolean`. If true, the node is listening for peers. If not, the node is disconnected from peers.

### Example

```text
ain.net.isListening();
```

## getNetworkId

```text
ain.net.getNetworkId()
```

### Returns

`Promise` returns a `String`.

### Example

```text
ain.net.getNetworkId(); // 'Testnet'
```

## getProtocolVersion

```text
ain.net.getProtocolVersion()
```

### Returns

`Promise` returns a `String`.

### Example

```text
ain.net.getProtocolVersion(); // "0.1.0"
```

## checkProtocolVersion

```text
ain.net.checkProtocolVersion()
```

### Returns

`Promise` returns an `Object`.

| Name | Type | Description |
| :--- | :--- | :--- |
| code | Number | 1 \(invalid\) or 0 \(valid\) |
| message | String | An error or a success message. |

### Example

```text
ain.net.checkProtocolVersion(); // "0.1.0"
```

## getPeerCount

```text
ain.net.getPeerCount()
```

### Returns

`Promise` returns a `Number`.

| Name | Type | Description |
| :--- | :--- | :--- |
| peerCount | Number | Number of peers the node is connected to. |

### Example

```text
ain.net.getPeerCount();
```

## isSyncing

```text
ain.net.isSyncing()
```

### Returns

`Promise` returns a `Boolean`.

| Name | Type | Description |
| :--- | :--- | :--- |
| syncing | Boolean | Whether the connected node is syncing with the blockchain. |

### Example

```text
ain.net.isSyncing();
```

