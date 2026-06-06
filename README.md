# DiceBot2

DiceBot2 is the fresh MVP implementation for the cross-platform dice bot project.

This first development pass focuses on a directly runnable command-line core before the Avalonia desktop UI is added. The code is structured so the same engine can later be used by the GUI, the Lua Programmer Mode, the DuckDice adapter, the high-speed executor, persistence, and the universal casino interface mapper.

## Implemented in this first pass

- .NET 8 console application.
- Core dice betting domain model.
- Built-in strategies:
  - flat betting
  - Martingale
  - Fibonacci
  - d'Alembert
  - preset list
  - Zig-Zag direction wrapper
- Deterministic simulation engine.
- Monte Carlo simulation runner.
- Lua Programmer Mode using MoonSharp.
- Seuntjie-style `dobet()` lifecycle for simulations.
- Lua variables: `balance`, `profit`, `wins`, `losses`, `bets`, `currentstreak`, `previousbet`, `previousprofit`, `win`, `nextbet`, `chance`, `bethigh`, `stop`.
- Safety-gated Lua functions: `withdraw`, `tip`, and `invest` are blocked unless explicitly enabled in host options.
- DuckDice REST API adapter skeleton.
- High-speed parallel executor skeleton.
- Universal casino interface mapping data model.

## Run

```bash
cd dicebot2
dotnet restore
dotnet run --project src/DiceBot.Cli -- simulate --strategy martingale --balance 1 --bets 1000 --basebet 0.00000001 --chance 49.5
```

Run Lua Programmer Mode simulation:

```bash
dotnet run --project src/DiceBot.Cli -- lua --script examples/martingale.lua --balance 1 --bets 1000 --basebet 0.00000001 --chance 49.5
```

Run Monte Carlo simulation:

```bash
dotnet run --project src/DiceBot.Cli -- montecarlo --strategy martingale --balance 1 --bets 1000 --basebet 0.00000001 --chance 49.5 --trials 100
```

Create an example universal casino mapping file:

```bash
dotnet run --project src/DiceBot.Cli -- mapper-template --name example --url https://example.com
```

## Safety

This project is gambling automation software. It must not claim that a strategy beats the house edge. Always test strategies with simulations before live use. Third-party Lua scripts are unsafe unless reviewed. Fund-moving functions remain disabled by default.
