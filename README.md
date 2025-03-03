# EGD

An Entropy Gathering Daemon (EGD) written in Python 3.

EGD requires Python 3.2 or later.

## Command-Line Usage

The EGD daemon can be controlled through various command-line options:

### Basic Operations

```bash
egd --start         # Start the daemon
egd --stop          # Stop the daemon gracefully
egd --status        # Check daemon status and entropy statistics
```

### Advanced Options

#### Starting with Force

```bash
egd --start --force  # Start daemon even if lock file exists
```
⚠️ Use with caution - only when you're sure no other instance is running

#### Managing Entropy

```bash
# Get 32 bytes of entropy (256 bits, suitable for an AES key)
egd --getentropy 32 > key.bin

# Get 64 bytes of entropy (512 bits)
egd --getentropy 64 > large_key.bin
```

**Note:** If insufficient entropy is available, fewer bytes than requested may be returned to maintain quality.

#### Manual Pool Persistence

```bash
egd --persist  # Manually save entropy pool to disk
```

### Common Usage Patterns

1. **System Boot**
   - Start the daemon: `egd --start`

2. **Regular Operation**
   - Check status: `egd --status`
   - Request entropy: `egd --getentropy N`

3. **System Shutdown**
   - Stop daemon: `egd --stop`

### Use Cases

- **Cryptographic Key Generation**
  ```bash
  egd --getentropy 32 > crypto.key
  ```

- **Random Number Generator Seeding**
  ```bash
  egd --getentropy 16 > rng_seed.bin
  ```

- **System Maintenance**
  ```bash
  egd --persist   # Backup entropy pool
  egd --stop      # Stop daemon
  # ... perform maintenance ...
  egd --start     # Restart daemon
  ```

## Author

Fran Litterio  
flitterio -at- gmail -dot- com
