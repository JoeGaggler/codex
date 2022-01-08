# Session Traversal Utilities for NAT
[rfc5389](https://datatracker.ietf.org/doc/html/rfc5389)
[rfc8489](https://datatracker.ietf.org/doc/html/rfc8489)

public stun servers:
* `stun1.l.google.com:19302`
* `stun2.l.google.com:19302`
* `stun3.l.google.com:19302`

terms:
*reflexive transport address* - the "public" address
*message* - *request* or *indication*
*method* - must be *binding* (per RFC 8489)

## request
```
      0                   1                   2                   3
      0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
     +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
     |0 0|     STUN Message Type     |         Message Length        |
     +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
     |                         Magic Cookie                          |
     +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
     |                                                               |
     |                     Transaction ID (96 bits)                  |
     |                                                               |
     +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```

```c#
var buffer = new byte[] {
	0x00, 0x01,	// Binding request
	0x00, 0x00,	// Message length
	0x21, 0x12, 0xa4, 0x42, // magic cookie
	0x35, 0x30, 0x68, 0x72, 0x37, 0x55, 0x6e, 0x64, 0x62, 0x56, 0x73, 0x62 // TXID
};
```

transaction id is random

## response
```c#
var r = recv.Buffer;
var a = r[0..2];
var ml = r[2..4];
var cookie = r[4..8];
var rid = r[8..20];

var a1t = r[20..22]; // 0x0020 = XOR MAPPED ADDRESS
var a1l = r[22..24]; // length 8
var a1m = r[24..32]; // because length

var res = a1m[0]; // reserved 0
var pro = a1m[1]; // 1 = IPv4
var por = a1m[2..4]; // XOR'd Port 
var ipx = a1m[4..8]; // XOR'd IPv4

var port = GetPort(por);
var ip = GetIPAddress(ipx);
```

```c#
var buffer = new byte[] {
	0x01, 0x01,
	0x00, 0x0c, // message length (12 bytes)
	0x21, 0x12, 0xa4, 0x42, // magic cookie
	0x35, 0x30, 0x68, 0x72, 0x37, 0x55, 0x6e, 0x64, 0x62, 0x56, 0x73, 0x62, // TXID
	0x00, 0x20, // att-type, 0x0020 = XOR-MAPPED-ADDRESS
	0x00, 0x08, // att-length, 8 bytes
	0x00, // reserved 0
	0x01, // 1 = IPv4
	0xff, 0xee, // XOR'd Port
	0xb2, 0xc9, 0x2d, 0xc1 // XOR'd IPv4
```

## magic cookie:

> 0x2112A442 in network byte order (i.e. big endian)

```c#
static byte[] cookie() => new byte[] { 0x21, 0x12, 0xa4, 0x42 };
```

## attributes
```
      0                   1                   2                   3
      0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
     +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
     |         Type                  |            Length             |
     +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
     |                         Value (variable)                ....
     +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```

occur on 32-bit boundaries, must pad with 0
type - 
	0x0000-0x7FFF are comprehension-required
	0x8000 and 0xFFFF are comprehension-optional

0x0001 = MAPPED-ADDRESS
0x0020 = XOR-MAPPED-ADDRESS

### xor-mapped-address
port is xor'd with most-significant bytes of magic cookie
ipv4 is xor'd with the entire magic cookie

## snippets
```c#
static int GetPort(byte[] xport)
{
	var arr = Xor(xport, cookie()[0..2]);
	return (arr[0] << 8) + arr[1];
}

static IPAddress GetIPAddress(byte[] xaddr)
{
	return new IPAddress(Xor(xaddr, cookie()));
}

static byte[] Xor(byte[] a, byte[] b) => a.Zip(b, (i, j) => i ^ j).Select(i => (byte)i).ToArray();
```

## notes
must send a message in order to receive, e.g. stun, then retain socket for peer messages

reusing the port requires demultiplexing stun vs app layer messages

on my network the binding lasted about 35 minutes
