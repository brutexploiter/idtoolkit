# MongoDB ObjectID
A powerful command-line utility for working with MongoDB ObjectIDs. Decode existing ObjectIDs, encode components into new ObjectIDs, and generate ObjectIDs in bulk with flexible specifications.

## Features

- **Decode ObjectIDs**
  - Extract timestamp, machine ID, process ID, and counter
- **Encode Components**
  - Create valid ObjectIDs from individual components
- **Bulk Generation**
  - Generate multiple ObjectIDs using ranges/lists/files
  - Supports time ranges, machine ID lists, counter sequences

## Installation

1. **Download the script**
```bash
curl -O https://raw.githubusercontent.com/brutexploiter/idtoolkit/main/mongodb-objectid/mongoid
```
2. **Make executable**

```bash
chmod +x mongoid
```
3. **Verify installation**

```bash
./mongoid --version
mongoid v1.0.0
```

# Usage
## Basic Commands

```bash
# Decode an ObjectID
./mongoid decode 64d94e71ac90fbbf3b7b8c79

# Encode components to ObjectID
./mongoid encode -t 1672531200 -m 123456 -p 54321 -c 987654

# Generate ObjectIDs in bulk
./mongoid generate -t "2025-01-15T13:09:00Z..2025-01-15T13:09:01Z" \
  -m 123456..123458 \
  -o output.txt
```
## Command Reference
### Decode
```bash
./mongoid decode [OPTIONS] <ObjectID>

Options:
  -d, --debug    Show debug information
  -h, --help     Show help
```
### Encode
```bash
./mongoid encode [OPTIONS]

Required Options:
  -t, --time TIME      Unix timestamp (0-4294967295)
  -m, --machine ID     Machine ID (0-16777215)
  -p, --process ID     Process ID (0-65535)
  -c, --counter VAL    Counter value (0-16777215)
```
### Generate
```bash
./mongoid generate [OPTIONS]

Options:
  -t, --time SPEC      Time specification (file:, range, or list)
  -m, --machine SPEC   Machine ID specification (file:, range, or list)
  -p, --process SPEC   Process ID specification (file:, range, or list)
  -c, --counter SPEC   Counter specification (file:, range, or list)
  -o, --output FILE    Output file name
  -d, --debug          Show generation details
  -v, --verbose        Show progress updates
  -h, --help           Show help
```

## ObjectID Structure

MongoDB ObjectIDs are 24-character hexadecimal strings representing:

- **4 bytes**: Unix timestamp
- **5 bytes**: Process unique identifier
  - 3 bytes: Machine ID
  - 2 bytes: Process ID
- **3 bytes**: Counter (initialized to random value)

### Example:
`64d94e71ac90fbbf3b7b8c79`

| Segment   | Description                              |
|-----------|------------------------------------------|
| 64d94e71  | Timestamp (July 18, 2023 08:34:09 UTC)  |
| ac90fb    | Machine ID                               |
| bf3b      | Process ID                               |
| 7b8c79    | Counter                                  |
  

## License
This project is licensed under the Apache License 2.0 - see the [LICENSE](https://github.com/brutexploiter/IDToolkit/blob/main/LICENSE) file for details.
