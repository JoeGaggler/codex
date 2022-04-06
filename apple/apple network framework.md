# NWEndpoint
enum:
* hostPort - `NWEndpoint.hostPort(host: h, port: p)`
* service
* unix
* url

also has `interface: NWInterface?` property

since this is an enum, if you have one, you can recapture the host/port using `switch`

## NWEndpoint.Host

```swift
let host: NWEndpoint = NWEndpoint.Host("blah.com")
```

# NWParameters
has static properties for defaults:
* dtls - over udp
* udp
* tcp
* tls - over tcp

init options:
* `(dtls: ?)`
* `(dtls: ?, udp: ?)`
* `(quic: )`
* `(tls: ?)`
* `(tls: ?, tcp: ?)`

to reuse a socket, set `requiredLocalEndpoint = NWEndpoint`

to share with other connections, set `allowLocalEndpointReuse = true`
still can't listen from multiple at the same time
might just prevent disposing the binding after connection closed #todo

hack to force ipv4:
```swift
let ops: NWProtocolOptions = udpParams.defaultProtocolStack.internetProtocol
let ipOps = opt as! NWProtocolIP.Options
ipOps.version = .v4 // default: .any
```

# NWPath
after connection is ready, `localEndpoint` stores connection that can be reused

# NWConnection
note that this requires a remote endpoint, even if you just want to listen (why? #todo)

the only init that we should have to care about:
```swift
let remote: NWEndpoint = ...
let params: NWParameters = ...
let connection: NWConnection = NWConnection(to: remote, using: params)

connection.stateUpdateHandler = ... // required

connection.start(queue: DispatchQueue.main)
```

must set `stateUpdateHandler` before `start`

## stateUpdateHandler

states:
* setup - after `init`
* preparing - after `start`
* ready - preparation was successful

transitions (incomplete, only as i've observed so far in the happy path):
```
init:
-> setup

start:
setup -> preparing

start success:
preparing -> ready
```

### ready
has `currentPath: NWPath` 


## receive
one call to receive results in one call to the provided completion handler

for udp: the response is a datagram
for tcp, or others: read the docs again

completion: 
```swift
completion: @escaping (
  _ completeContent: Data?, 
  _ contentContext: NWConnection.ContentContext?, 
  _ isComplete: Bool, 
  _ error: NWError?
) -> Void
```

## send
multiple options, but the one i current use with udp:
```swift
send(
  content: data, 
  completion: NWConnection.SendCompletion.contentProcessed {error: NWError? in }
)
```
