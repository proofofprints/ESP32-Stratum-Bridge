# ESP32 Stratum Bridge for Kaspa

A modified Kaspa Stratum Bridge optimized for ESP32-based miners like [KASDeck](https://github.com/proofofprints/kasdeck).

This bridge acts as a translator between your local Kaspa node (kaspad) and ESP32 mining devices, allowing solo mining directly to your own node.

## Features

- **ESP32 Optimized**: Configured for low-difficulty shares suitable for ESP32 hashrates
- **Solo Mining**: Connect directly to your own Kaspa node
- **Low Share Difficulty**: Default `min_share_diff: 0.0001` for accurate hashrate reporting from low-power devices
- **Stratum Protocol**: Standard stratum mining protocol on port 5555
- **Stats & Logging**: Built-in statistics and file logging

## Based On

This is a modified version of [onemorebsmith/kaspa-stratum-bridge](https://github.com/onemorebsmith/kaspa-stratum-bridge) with configuration optimized for ESP32 miners.

## Quick Start

### Prerequisites

- A running Kaspa node (kaspad) with RPC enabled on port 16110
- Windows PC on the same network as your ESP32 miner

### Installation

1. Download `ks_esp32_bridge.zip` from the [Releases](https://github.com/proofofprints/ESP32-Stratum-Bridge/releases) page
2. Extract to a folder on your PC
3. Edit `config.yaml` if needed (defaults work for local node)
4. Run `ks_bridge_esp32.exe`

### Configuration

Edit `config.yaml` to customize:

```yaml
# Port for miners to connect to
stratum_port: :5555

# Your Kaspa node RPC address
kaspad_address: localhost:16110

# Share difficulty (lower = more shares, better for ESP32)
min_share_diff: 0.0001

# Enable stats display
print_stats: true

# Enable logging to file
log_to_file: true
```

### Connecting Your Miner

Configure your ESP32 miner (e.g., KASDeck) with:
- **Pool URL**: `stratum+tcp://YOUR_PC_IP:5555`
- **Wallet**: Your Kaspa wallet address

## Architecture

```
[ESP32 Miner] --stratum--> [Bridge:5555] --RPC--> [Kaspad:16110] --> [Kaspa Network]
```

## Troubleshooting

### Bridge can't connect to kaspad
- Ensure kaspad is running with RPC enabled
- Check that port 16110 is accessible
- Verify `kaspad_address` in config.yaml

### Miner can't connect to bridge
- Check Windows Firewall allows port 5555
- Verify the bridge is running (console window open)
- Ensure miner and PC are on the same network

### No shares being accepted
- Verify your wallet address is correct
- Check bridge logs for errors
- Ensure kaspad is fully synced

## Credits

- Original bridge by [onemorebsmith](https://github.com/onemorebsmith/kaspa-stratum-bridge)
- ESP32 modifications by [Proof of Prints](https://github.com/proofofprints)

## License

MIT License - See original repository for full license terms.
