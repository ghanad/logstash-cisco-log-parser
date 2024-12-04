# Cisco Logs Parser for Logstash

This repository contains Logstash configuration files for parsing Cisco device logs. It focuses on specific log patterns including login events and user commands while providing a general pattern for other log types.

## Features

- Parses Cisco device logs with specific patterns for:
  - Login success/failure events
  - User command execution logs
  - General system logs
- Handles various date formats commonly found in Cisco logs
- Converts numeric fields to appropriate types
- Timezone support for accurate timestamp parsing

## Repository Structure

```
.
├── patterns/
│   └── cisco_patterns              # Custom Grok patterns for Cisco logs
└── pipeline/
    └── cisco.conf                  # Logstash filter configuration
```

## Pattern Types

### 1. Login Events
Parses detailed information from login success/failure events including:
- Username
- Client IP
- Destination port
- Failure reason (if applicable)
- Timestamp

Example log:
```
<189>844: Dec  2 05:16:04: %SEC_LOGIN-5-LOGIN_SUCCESS: Login Success [user: admin] [Source: 192.168.1.58] [localport: 22] at 08:46:04 Tehran Fri Dec 2 2022
```

### 2. User Commands
Tracks command execution by users with details including:
- Username
- Executed command
- Timestamp

Example log:
```
<189>123: Dec 2 05:13:11: %SEC_CMD-5-COMMAND: User:admin logged command:show version
```

### 3. General Logs
Captures basic information from all other log types including:
- Priority
- Sequence ID
- Timestamp
- Facility
- Severity
- Event type
- Message

## Installation

1. Copy the `cisco_patterns` file to your Logstash patterns directory:
   ```bash
   cp patterns/cisco_patterns /etc/logstash/patterns/
   ```

2. Copy the pipeline configuration:
   ```bash
   cp pipeline/cisco.conf /etc/logstash/conf.d/
   ```

3. Restart Logstash to apply the changes:
   ```bash
   systemctl restart logstash
   ```

## Field Types

The following fields are automatically converted to integers:
- priority
- sequence_id
- severity
- destination_port

## Contributing

Feel free to submit issues, fork the repository, and create pull requests for any improvements.
