## PWR Chain GO SDK

PWR Go is a Go library for interacting with the PWR network.
It provides an easy interface for wallet management and sending transactions on PWR.

<div align="center">
<!-- markdownlint-restore -->

[![Pull Requests welcome](https://img.shields.io/badge/PRs-welcome-ff69b4.svg?style=flat-square)](https://github.com/pwrlabs/pwrgo/issues?q=is%3Aissue+is%3Aopen+label%3A%22help+wanted%22)
[![go-badge](https://pkg.go.dev/badge/github.com/pwrlabs/pwrgo)](https://pkg.go.dev/github.com/pwrlabs/pwrgo)
<a href="https://github.com/pwrlabs/pwrgo/blob/main/LICENSE/">
  <img src="https://img.shields.io/badge/license-MIT-black">
</a>
<!-- <a href="https://github.com/pwrlabs/pwrgo/stargazers">
  <img src='https://img.shields.io/github/stars/pwrlabs/pwrgo?color=yellow' />
</a> -->
<a href="https://pwrlabs.io/">
  <img src="https://img.shields.io/badge/powered_by-PWR Chain-navy">
</a>
<a href="https://www.youtube.com/@pwrlabs">
  <img src="https://img.shields.io/badge/Community%20calls-Youtube-red?logo=youtube"/>
</a>
<a href="https://twitter.com/pwrlabs">
  <img src="https://img.shields.io/twitter/follow/pwrlabs?style=social"/>
</a>

</div>

## 🌐 Documentation

How to [Guides](https://docs.pwrlabs.io/pwrchain/overview) 🔜 & [API](https://docs.pwrlabs.io/developers/developing-on-pwr-chain/what-is-a-decentralized-application) 💻

Play with [Code Examples](https://github.com/keep-pwr-strong/pwr-examples/) 🎮

## 💫 Getting Started

**Import the library:**

```go
import (
    "fmt"
    "github.com/pwrlabs/pwrgo/rpc"
    "github.com/pwrlabs/pwrgo/wallet"
)
```

**Set your RPC node:**

```go
var pwr = rpc.SetRpcNodeUrl("https://pwrrpc.pwrlabs.io")
```

**Generate a new random wallet:**

```go
wallet, _ := wallet.NewRandom(12)
```

**Import wallet by Seed Phrase:**

```go
seedPhrase := "your seed phrase here"
wallet, _ := wallet.New(seedPhrase)
```

**Get wallet address:**

```go
var address = wallet.GetAddress()
```

**Get wallet seed phrase:**

```go
var seedPhrase = wallet.GetSeedPhrase()
```

**Get wallet balance:**

```go
var balance = wallet.GetBalance()
```

**Transfer PWR tokens:**

```go
wallet.TransferPWR("recipientAddress", "amount", "feePerByte")
```

Sending a transcation to the PWR Chain returns a Response object, which specified if the transaction was a success, and returns relevant data.
If the transaction was a success, you can retrieive the transaction hash, if it failed, you can fetch the error.

```go
package main
import (
    "fmt"
    "github.com/pwrlabs/pwrgo/rpc"
    "github.com/pwrlabs/pwrgo/wallet"
)
func main() {
    seedPhrase := "your seed phrase here"
    wallet, _ := wallet.New(seedPhrase)

    amount := 1000
    feePerByte := wallet.GetRpc().GetFeePerByte()

    response := wallet.TransferPWR("recipientAddress", amount, feePerByte)
    if response.Success {
        fmt.Printf("Transfer tx hash: %s\n", response.Hash)
    } else {
        fmt.Println("Error sending Transfer tx:", response.Error)
    }
}
```

**Send data to a VIDA:**

```go
package main
import (
    "fmt"
    "github.com/pwrlabs/pwrgo/rpc"
    "github.com/pwrlabs/pwrgo/wallet"
)
func main() {
    seedPhrase := "your seed phrase here"
    wallet, _ := wallet.New(seedPhrase)

    vidaId := 123
    data := []byte("Hello world")
    feePerByte := wallet.GetRpc().GetFeePerByte()

    response := wallet.SendVidaData(vidaId, data, feePerByte)
    if response.Success {
        fmt.Printf("Sending tx hash: %s\n", response.Hash)
    } else {
        fmt.Println("Error sending VIDA data tx:", response.Error)
    }
}
```

### Other Static Calls

**Get RPC Node Url:**

Returns currently set RPC node URL.

```go
var url = pwr.GetRpcNodeUrl()
```

**Get Fee Per Byte:**

Gets the latest fee-per-byte rate.

```go
var fee = pwr.GetFeePerByte()
```

**Get Balance Of Address:**

Gets the balance of a specific address.

```go
var balance = pwr.GetBalanceOfAddress("0x...")
```

**Get Nonce Of Address:**

Gets the nonce/transaction count of a specific address.

```go
var nonce = pwr.GetNonceOfAddress("0x...")
```

## ✏️ Contributing

If you consider to contribute to this project please read [CONTRIBUTING.md](https://github.com/pwrlabs/pwrgo/blob/main/CONTRIBUTING.md) first.

You can also join our dedicated channel for [developers](https://discord.com/channels/1141787507189624992/1180224756033790014) on the [PWR Chain Discord](https://discord.com/invite/YASmBk9EME)

## 📜 License

Copyright (c) 2025 PWR Labs

Licensed under the [MIT license](https://github.com/pwrlabs/pwrgo/blob/main/LICENSE).
