# HTTP Traffic Analysis: Tracing an Image Download

## Goal

Examine a small packet capture in Wireshark and explain what the client requested, what the server returned, and what the capture can and cannot establish.

## Tools

- Wireshark for inspecting frames, TCP traffic, and HTTP headers
- Packet capture supplied for a practice exercise (the capture itself is not included here)

## Method

1. Open the capture and review the protocol and packet list. It contains 40 Ethernet/IPv4 packets in one TCP conversation.
2. Locate the HTTP request to the server on TCP port 80 and inspect the request line, `Host`, and `User-Agent` headers.
3. Locate the matching HTTP response. Inspect its status code, content type, and declared content length.
4. Follow the TCP stream to connect the request with the response and image data. Separate what appears in the capture from assumptions about the client's intent.

## Observations

| Evidence | Observation |
| --- | --- |
| Request | `GET /images/layout/logo.png HTTP/1.0` |
| Host header | `packetlife.net` |
| User-Agent | `Wget/1.12 (linux-gnu)` |
| Response | `HTTP/1.1 200 OK` |
| Content-Type | `image/png` |
| Content-Length | `21684` bytes, as declared by the server |

The request used HTTP on port 80. The `linux-gnu` string describes the client software's reported platform; it does not independently prove the operating system of the computer. A `200 OK` response indicates the server accepted the request and sent a response. The content length above comes from the header, rather than a separate verification of the extracted file.

## Conclusion

The capture shows a client requesting a PNG image and the server returning an HTTP success response with image content. This alone does not show an attack or compromise. Because this is unencrypted HTTP, the request path and headers are visible in the capture.

## Sharing note

This write-up intentionally omits the original capture, challenge questions, answers, and any flags. Review the exercise or competition sharing rules before adding screenshots or source files.
