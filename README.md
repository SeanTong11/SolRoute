# SolRoute SDK

SolRoute is a Go SDK that serves as the fundamental infrastructure for building DEX routing services on Solana. Unlike solutions that rely on third-party APIs, SolRoute directly interacts with the Solana blockchain.

## Features

- **Protocol Support**
  - Raydium CPMM V4 (`675kPX9MHTjS2zt1qfr1NYHuzeLXfQM9H24wFSUt1Mp8`)
  - Raydium CPMM (`CPMMoo8L3F4NbTegBCKVNunggL7H1ZpdTHKxQB5qKP1C`)
  - Raydium CLMM (`CAMMCzo5YL8w4VFF8KVHrK22GGUsp5VTaW7grrKgrWqK`)
  - PumpSwap AMM (`pAMMBay6oceH9fJKBRHGP5D4bD4sWpmSwMn52FMfXEA`)
  - Meteora DLMM (`LBUZKhRxPF3XUpBCjp4YzTKgLccjZhTSDM9YuVaPwxo`)

- **Core Functionality**
  - Pool discovery and management
  - Quote generation
  - Cross-DEX routing and optimal path finding
  - Transaction instruction building

## Quick Start

```go
// Initialize router with supported protocols
router := router.NewSimpleRouter(
    protocol.NewPumpAmm(solClient),
    protocol.NewRaydiumAmm(solClient),
    protocol.NewRaydiumClmm(solClient),
    protocol.NewRaydiumCpmm(solClient),
)

// Find best pool and execute swap
bestPool, amountOut, err := router.GetBestPool(ctx, solClient.RpcClient, 
    "TOKEN0_MINT", "TOKEN1_MINT", amountIn)
if err != nil {
    log.Fatal(err)
}

// Build and send transaction
instructions, err := bestPool.BuildSwapInstructions(ctx, solClient.RpcClient,
    userPublicKey, "TOKEN0_MINT", amountIn, minAmountOut)
```

## Installation

```bash
go get github.com/yimingWOW/solroute
```

## Project Structure

```
solroute/
├── pkg/
│   ├── api/         # Core interfaces
│   ├── pool/        # Pool implementations
│   ├── protocol/    # DEX implementations
│   ├── router/      # Routing engine
│   └── sol/         # Solana client
```

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.