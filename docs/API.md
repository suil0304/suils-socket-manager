# suils-socket-manager api
great
----------------------------

# Manager
## SuilSocketManager
*`extends funkin.modding.module.Module`*

- ***id: suil-socket-manager"***
- ***priority: 1***

### Fields
#### CONNECT
*alias of enum [`TCPSocketEventType.CONNECT`](../suil0304/socket/event/tcp/TCPSocketEventType.hxc)*

TCP Connect Event.

Listener parameter should be [`SocketConnectEvent`](../suil0304/socket/event/tcp/SocketConnectEvent.hxc).

#### DATA
*alias of enum [`TCPSocketEventType.DATA`](../suil0304/socket/event/tcp/TCPSocketEventType.hxc)*

TCP Data Received Event.

Listener parameter should be [`SocketDataEvent`](../suil0304/socket/event/tcp/SocketDataEvent.hxc).

#### CLOSE
*alias of enum [`TCPSocketEventType.CLOSE`](../suil0304/socket/event/tcp/TCPSocketEventType.hxc)*

TCP Close Event.

Listener parameter should be [`SocketCloseEvent`](../suil0304/socket/event/tcp/SocketCloseEvent.hxc).

#### CONNECT_TIMEOUT
*alias of enum [`TCPSocketEventType.CONNECT_TIMEOUT`](../suil0304/socket/event/tcp/TCPSocketEventType.hxc)*

TCP Connect Timeout Event.

Listener parameter should be [`SocketTimeoutEvent`](../suil0304/socket/event/tcp/SocketTimeoutEvent.hxc).

#### REFRESH_TIMEOUT
*alias of enum [`TCPSocketEventType.REFRESH_TIMEOUT`](../suil0304/socket/event/tcp/TCPSocketEventType.hxc)*

TCP Refresh Timeout Event.

Listener parameter should be [`SocketTimeoutEvent`](../suil0304/socket/event/tcp/SocketTimeoutEvent.hxc).

### Methods
#### createSocket
Create TCP socket.

No connect call.

##### Parameters
| Name | Type | Description |
| --- | --- | --- |
| `id` | `String` | Socket's id |
| `contract` | [`TCPCustomContract`](../suil0304/socket/contract/TCPCustomContract.hxc) | Your custom contract |

#### connectSocket
Connect TCP socket.

You should create your socket first.

##### Parameters
| Name | Type | Description |
| --- | --- | --- |
| `id` | `String` | Socket's id |
| `host` | `String` | Server address (like "127.0.0.1") |
| `port` | `Int` | Server port |

##### Returns
`Bool`

If connect called successfully, it returns true.
Else, it returns false.

#### closeSocket
Close TCP socket.

You should create your socket first.

No destroy.

##### Parameters
| Name | Type | Description |
| --- | --- | --- |
| `id` | `String` | Socket's id |

##### Returns
`Bool`

If closed successfully, it returns true.
Else, it returns false.

#### destroySocket
Destroy TCP socket.

It removes socket in socketMap too.

##### Parameters
| Name | Type | Description |
| --- | --- | --- |
| `id` | `String` | Socket's id |

##### Returns
`Bool`

If destroyed successfully, it returns true.
Else, it returns false.

#### sendBytes
Send to server your texts.

##### Parameters
| Name | Type | Description |
| --- | --- | --- |
| `id` | `String` | Socket's id |
| `header` | `StringMap<Dynamic>` | Your custom contract header |
| `text` | `String` | Your text |

##### Returns
`Bool`

If sent successfully, it returns true.
Else, it returns false.

#### addEventListener
Add your event listener into socket.

##### Parameters
| Name | Type | Description |
| --- | --- | --- |
| `id` | `String` | Socket's id |
| `socketEvent` | `Int` | Please use SocketEvents, I'm so sad. |
| `listener` | `Dynamic->Void` | Your event listener |
| `priority` | `Int` | Event listener priority (ASC) |

##### Returns
`Bool`

If added successfully, it returns true.
Else, it returns false.

#### removeEventListener
Remove your event listener in socket.

##### Parameters
| Name | Type | Description |
| --- | --- | --- |
| `id` | `String` | Socket's id |
| `socketEvent` | `Int` | Please use SocketEvents, I'm so sad. |
| `listener` | `Dynamic->Void` | Your event listener |

##### Returns
`Bool`

If removed successfully, it returns true.
Else, it returns false.

#### willTrigger
Check if this event have listener(s).

No dispatch listeners.

##### Parameters
| Name | Type | Description |
| --- | --- | --- |
| `id` | `String` | Socket's id |
| `socketEvent` | `Int` | Please use SocketEvents, I'm so sad. |

##### Returns
`Bool`

If it have its listener(s), it returns true.
Else, it returns false.

## SuilSocketManager
*`extends funkin.modding.module.Module`*

WIP

- ***id: suil-udp-socket-manager"***
- ***priority: 2***

### Fields
#### CONNECT
*alias of enum [`SocketEventType.CONNECT`](../suil0304/socket/event/SocketEventType.hxc)*

UDP Connect Event.

not worked

Listener parameter should be [`UDPSocketConnectEvent`](../suil0304/socket/event/udp/UDPSocketConnectEvent.hxc).

#### DATA
*alias of enum [`SocketEventType.DATA`](../suil0304/socket/event/SocketEventType.hxc)*

UDP Data Received Event.

Listener parameter should be [`UDPSocketDataEvent`](../suil0304/socket/event/udp/UDPSocketDataEvent.hxc).

#### CLOSE
*alias of enum [`SocketEventType.CLOSE`](../suil0304/socket/event/SocketEventType.hxc)*

UDP Close Event.

Listener parameter should be [`UDPSocketCloseEvent`](../suil0304/socket/event/udp/UDPSocketCloseEvent.hxc).

### Methods
#### createSocket
Create UDP socket.

No connect call.

##### Parameters
| Name | Type | Description |
| --- | --- | --- |
| `id` | `String` | Socket's id |

#### bindSocket
Bind UDP socket.

You should create your socket first.

##### Parameters
| Name | Type | Description |
| --- | --- | --- |
| `id` | `String` | Socket's id |
| `localPort` | `Int` | Local port |
| `localAddress` | `String` | Local address (like "127.0.0.1") |

##### Returns
`Bool`

If bound successfully, it returns true.
Else, it returns false.

#### closeSocket
Close UDP socket.

You should create your socket first.

Same as destroy. It removes socket in socketMap.

##### Parameters
| Name | Type | Description |
| --- | --- | --- |
| `id` | `String` | Socket's id |

##### Returns
`Bool`

If closed successfully, it returns true.
Else, it returns false.

#### send
Send to server your texts.

##### Parameters
| Name | Type | Description |
| --- | --- | --- |
| `id` | `String` | Socket's id |
| `text` | `String` | Your text |
| `address` | `Null<String>` | Server address (like "127.0.0.1") |
| `port` | `Int` | Server port |

##### Returns
`Bool`

If sent successfully, it returns true.
Else, it returns false.

#### receive
Receive to server your texts.

WIP

##### Parameters
| Name | Type | Description |
| --- | --- | --- |
| `id` | `String` | Socket's id |

##### Returns
`Bool`

If received successfully, it returns true.
Else, it returns false.

#### addEventListener
Add your event listener into socket.

##### Parameters
| Name | Type | Description |
| --- | --- | --- |
| `id` | `String` | Socket's id |
| `socketEvent` | `Int` | Please use SocketEvents, I'm so sad. |
| `listener` | `Dynamic->Void` | Your event listener |
| `priority` | `Int` | Event listener priority (ASC) |

##### Returns
`Bool`

If added successfully, it returns true.
Else, it returns false.

#### removeEventListener
Remove your event listener in socket.

##### Parameters
| Name | Type | Description |
| --- | --- | --- |
| `id` | `String` | Socket's id |
| `socketEvent` | `Int` | Please use SocketEvents, I'm so sad. |
| `listener` | `Dynamic->Void` | Your event listener |

##### Returns
`Bool`

If removed successfully, it returns true.
Else, it returns false.

#### willTrigger
Check if this event have listener(s).

No dispatch listeners.

##### Parameters
| Name | Type | Description |
| --- | --- | --- |
| `id` | `String` | Socket's id |
| `socketEvent` | `Int` | Please use SocketEvents, I'm so sad. |

##### Returns
`Bool`

If it have its listener(s), it returns true.
Else, it returns false.

## SuilContractManager
*`extends funkin.modding.module.Module`*

TCP only

- ***id: suil-udp-socket-manager"***
- ***priority: 0***

### Fields
#### BYTE_HEADER_TYPE
*alias of enum [`HeaderType.BYTE`](../suil0304/socket/contract/constants/HeaderType.hxc)*

Set header's type to byte.

Byte size fixed at 1.

#### SHORT_HEADER_TYPE
*alias of enum [`HeaderType.SHORT`](../suil0304/socket/contract/constants/HeaderType.hxc)*

Set header's type to short.

Byte size fixed at 2.

#### INT_HEADER_TYPE
*alias of enum [`HeaderType.INT`](../suil0304/socket/contract/constants/HeaderType.hxc)*

Set header's type to int.

Byte size fixed at 4.

#### VARINT_HEADER_TYPE
*alias of enum [`HeaderType.VARINT`](../suil0304/socket/contract/constants/HeaderType.hxc)*

Set header's type to variable int.

WIP

#### STRING_HEADER_TYPE
*alias of enum [`HeaderType.STRING`](../suil0304/socket/contract/constants/HeaderType.hxc)*

Set header's type to string.

#### PAYLOAD_BYTE_SIZE_HEADER_ROLE
*alias of enum [`HeaderType.PAYLOAD_BYTE_SIZE`](../suil0304/socket/contract/constants/HeaderRole.hxc)*

Set header's role to payload byte size.

(Unique role)

### Methods
#### createTCPContractBuilder
Create TCPContractBuilder.

##### Returns
[`TCPContractBuilder`](../suil0304/socket/contract/builder/TCPContractBuilder.hxc)

Set contract up and build it.

#### setTCPContract
Save your tcp contract(s).

##### Parameters
| Name | Type | Description |
| --- | --- | --- |
| `id` | `String` | Contract's id |
| `contract` | [`TCPCustomContract`](../suil0304/socket/contract/TCPCustomContract.hxc) | Your tcp contract |

##### Returns
`Bool`

If set successfully, it returns true.
Else, it returns false.

#### getTCPContract
Get it.

##### Parameters
| Name | Type | Description |
| --- | --- | --- |
| `id` | `String` | Contract's id |

##### Returns
`Null<`[`TCPCustomContract`](../suil0304/socket/contract/TCPCustomContract.hxc)`>`

Your tcp contract.

#### getTCPContractDefault
Get default tcp contract.

##### Returns
[`TCPCustomContract`](../suil0304/socket/contract/TCPCustomContract.hxc)

Your tcp contract.

# Event
## SocketEventBase
*`package suil0304.socket.event`*

### Fields
#### localAddress
`String`

Socket's local address.

#### localPort
`Int`

Socket's local port.

#### shouldPropagate
`Bool`

***null setter***

This event should propagate?

### Methods
#### stopPropagation
Stop propagation.

## SocketConnectEvent
*`package suil0304.socket.event.tcp`*

*`extends `[`SocketEventBase`](../suil0304/socket/event/SocketEventBase.hxc)*

### Fields
#### remoteAddress
`String`

***null setter***

Server address.

#### remotePort
`Int`

***null setter***

Server port.

## SocketDataEvent
*`package suil0304.socket.event.tcp`*

*`extends `[`SocketEventBase`](../suil0304/socket/event/SocketEventBase.hxc)*

### Fields
#### headerMap
[`ReadonlyStringMap`](../suil0304/ds/ReadonlyStringMap.hxc)

***null setter***

Your tcp header map.

#### remotePort
[`ReadonlyArray`](../suil0304/ds/ReadonlyArray.hxc) (Maybe `String`)

***null setter***

Ordered array of headers.

#### payloadString
`String`

***null setter***

Payload Thingie. (Not ByteArray)

## SocketCloseEvent
*`package suil0304.socket.event.tcp`*

*`extends `[`SocketEventBase`](../suil0304/socket/event/SocketEventBase.hxc)*

Nothing

## SocketTimeoutEvent
*`package suil0304.socket.event.tcp`*

*`extends `[`SocketEventBase`](../suil0304/socket/event/SocketEventBase.hxc)*

Nothing

## UDPSocketConnectEvent
*`package suil0304.socket.event.udp`*

*`extends `[`SocketEventBase`](../suil0304/socket/event/SocketEventBase.hxc)*

### Fields
#### remoteAddress
`String`

***null setter***

Server address.

#### remotePort
`Int`

***null setter***

Server port.

## UDPSocketDataEvent
*`package suil0304.socket.event.udp`*

*`extends `[`SocketEventBase`](../suil0304/socket/event/SocketEventBase.hxc)*

### Fields
#### data
`String`

***null setter***

Your received data. (Not ByteArray)

## UDPSocketCloseEvent
*`package suil0304.socket.event.udp`*

*`extends `[`SocketEventBase`](../suil0304/socket/event/SocketEventBase.hxc)*

Nothing

# Builder
## TCPContractBuilder
*`package suil0304.socket.contract.builder`*

### Methods
#### setConnectTimeout
Set your connect timeout.

##### Parameters
| Name | Type | Description |
| --- | --- | --- |
| `ms` | `Int` | Timeout max |

##### Returns
[`TCPContractBuilder`](../suil0304/socket/contract/builder/TCPContractBuilder.hxc)

Chaining Method

#### setRefreshTimeout
Set your refresh timeout.

##### Parameters
| Name | Type | Description |
| --- | --- | --- |
| `ms` | `Int` | Timeout max |

##### Returns
[`TCPContractBuilder`](../suil0304/socket/contract/builder/TCPContractBuilder.hxc)

Chaining Method

#### addHeader
Add header and set current header index to this.

##### Returns
[`TCPContractBuilder`](../suil0304/socket/contract/builder/TCPContractBuilder.hxc)

Chaining Method

#### setHeaderIndex
Add header and set current header index to this.

##### Parameters
| Name | Type | Description |
| --- | --- | --- |
| `index` | `Int` | New current header index |

##### Returns
[`TCPContractBuilder`](../suil0304/socket/contract/builder/TCPContractBuilder.hxc)

Chaining Method

#### popHeader
Remove last header and change current header index (if index == last header).

##### Returns
[`TCPContractBuilder`](../suil0304/socket/contract/builder/TCPContractBuilder.hxc)

Chaining Method

#### setHeaderName
Set your header's name.

(Required)

##### Parameters
| Name | Type | Description |
| --- | --- | --- |
| `name` | `Int` | Your header's name |

##### Returns
[`TCPContractBuilder`](../suil0304/socket/contract/builder/TCPContractBuilder.hxc)

Chaining Method

#### setHeaderType
Set your header's type.

(Required)

##### Parameters
| Name | Type | Description |
| --- | --- | --- |
| `type` | `Int` | please use [this](../suil0304/socket/contract/constants/HeaderType.hxc) |

##### Returns
[`TCPContractBuilder`](../suil0304/socket/contract/builder/TCPContractBuilder.hxc)

Chaining Method

#### setHeaderByteSize
Set your header's byte size.

(Required on VARINT and STRING)

##### Parameters
| Name | Type | Description |
| --- | --- | --- |
| `byteSize` | `Int` | Your header's byte size |

##### Returns
[`TCPContractBuilder`](../suil0304/socket/contract/builder/TCPContractBuilder.hxc)

Chaining Method

#### addHeaderRole
Add role to your header.

IT MUST HAVE ONCE PAYLOAD BYTE SIZE ROLE!

##### Parameters
| Name | Type | Description |
| --- | --- | --- |
| `role` | `Int` | please use [this](../suil0304/socket/contract/constants/HeaderRole.hxc) |

##### Returns
[`TCPContractBuilder`](../suil0304/socket/contract/builder/TCPContractBuilder.hxc)

Chaining Method

#### resetHeaderRole
Reset header's role.

##### Returns
[`TCPContractBuilder`](../suil0304/socket/contract/builder/TCPContractBuilder.hxc)

Chaining Method

#### setConnectedMessage
Set your connected message.

##### Parameters
| Name | Type | Description |
| --- | --- | --- |
| `message` | `String` | Your handshake message |

##### Returns
[`TCPContractBuilder`](../suil0304/socket/contract/builder/TCPContractBuilder.hxc)

Chaining Method

#### setCloseMessage
Set your close message.

##### Parameters
| Name | Type | Description |
| --- | --- | --- |
| `message` | `String` | Your handshake message |

##### Returns
[`TCPContractBuilder`](../suil0304/socket/contract/builder/TCPContractBuilder.hxc)

Chaining Method

#### build
Build it.

##### Returns
[`TCPCustomContract`](../suil0304/socket/contract/TCPCustomContract.hxc)

If built successfully, it returns contract.
Else, you will get error.
