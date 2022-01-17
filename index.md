---
layout: default
---
[![build](https://github.com/go-lark/lark/actions/workflows/ci.yml/badge.svg)](https://github.com/go-lark/lark/actions/workflows/ci.yml)
[![codecov](https://codecov.io/gh/go-lark/lark/branch/main/graph/badge.svg)](https://codecov.io/gh/go-lark/lark)
[![Go Report Card](https://goreportcard.com/badge/github.com/go-lark/lark)](https://goreportcard.com/report/github.com/go-lark/lark)
[![Go Reference](https://pkg.go.dev/badge/github.com/go-lark/lark.svg)](https://pkg.go.dev/github.com/go-lark/lark)
[![Mentioned in Awesome Go](https://awesome.re/mentioned-badge.svg)](https://github.com/avelino/awesome-go)

An easy-to-use unofficial SDK for Feishu and Lark Open Platform.

go-lark implements messaging APIs, with full-fledged supports on building Chat Bot and Notification Bot.

It is widely used and tested by in-house ~450 developers with over 1.5k Go packages.

## Features

- Notification bot & chat bot supported
- Send messages (Group, Private, Rich Text, and Card)
- Quick to build message with `MsgBuffer`
- Easy to create incoming message hook
- Encryption and token verification supported
- Middleware support for Gin web framework
- Highly extensible
- Documentation & tests

## Installation

```shell
go get github.com/go-lark/lark
```

## Quick Start

### Prerequisite

There are two types of bot that is supported by go-lark. We need to create a bot manually.

Chat Bot:

- Feishu: create from [Feishu Open Platform](https://open.feishu.cn/).
- Lark: create from [Lark Developer](https://open.larksuite.com/).
- App ID and App Secret are required to init a `ChatBot`.

Notification Bot:

- Create from group chat.
- Web Hook URL is required.

### Sending Message

Chat Bot:

```go
import "github.com/go-lark/lark"

func main() {
    bot := lark.NewChatBot("<App ID>", "<App Secret>")
    bot.StartHeartbeat()
    bot.PostText("hello, world", lark.WithEmail("someone@example.com"))
}
```

Notification Bot:

```go
import "github.com/go-lark/lark"

func main() {
    bot := lark.NewNotificationBot("<WEB HOOK URL>")
    bot.PostNotification("title", "text")
}
```

## Limits

- go-lark is tested on Feishu endpoints, which literally compats Lark endpoints,
  because Feishu and Lark basically shares the same API specification.
  We do not guarantee all of the APIs work well with Lark, until we have tested it on Lark.
- go-lark only supports Custom App. Marketplace App is not supported yet.
- go-lark implements bot and messaging API, other APIs such as Lark Doc, Calendar and so so are not supported.

### Switch to Lark Endpoints

The default API endpoints are for Feishu, in order to switch to Lark, we should use `SetDomain`:

```go
bot := lark.NewChatBot("<App ID>", "<App Secret>")
bot.SetDomain(lark.DomainLark)
```

## Documentation

See full documentation [on README](https://github.com/go-lark/lark/blob/main/README.md).
