I've created a comprehensive README.md file for your Git repository that explains the OS Update workflow:

# Automated OS Update Workflow

![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-2088FF?style=for-the-badge&logo=github-actions&logoColor=white)
![Ubuntu](https://img.shields.io/badge/Ubuntu-E95420?style=for-the-badge&logo=ubuntu&logoColor=white)

A GitHub Actions workflow that automates secure and reliable OS updates for Ubuntu/Debian servers. This workflow connects to a remote server via SSH and performs a complete system update with comprehensive error handling and reporting.

## 🚀 Features

- **Automated Package Updates**: Schedule regular updates or run manually
- **Safe Concurrency**: Prevents multiple simultaneous updates
- **Disk Space Verification**: Ensures sufficient space before updates
- **Comprehensive Updates**: Uses `dist-upgrade` and `autoremove` for thorough system maintenance
- **Detailed Reporting**: Provides update summaries including packages changed
- **Intelligent Reboot Handling**: Optional automatic reboots when required
- **Built-in Safety Measures**: Prevents failed or incomplete updates

## 📋 Prerequisites

- A GitHub repository where you'll store this workflow
- An Ubuntu/Debian server with SSH access
- GitHub repository secrets configured for SSH access

## ⚙️ Setup Instructions

1. Add this workflow file to your repository at `.github/workflows/os-update.yml`

2. Configure the following repository secrets:
   - `SSH_HOST` - The hostname or IP of your server
   - `SSH_USERNAME` - SSH username
   - `SSH_PRIVATE_KEY` - SSH private key for authentication

3. Configure the workflow environment variables as needed:
   - `RUN_OS_UPDATE` - Set to "true" to enable scheduled runs
   - `REBOOT_IF_NEEDED` - Set to "true" to allow automatic reboots

## 📝 Configuration Options

### Environment Variables

| Variable | Default | Description |
|----------|---------|-------------|
| `RUN_OS_UPDATE` | "false" | Enable/disable scheduled updates |
| `REBOOT_IF_NEEDED` | "false" | Enable/disable automatic reboots |

### Scheduling

By default, the workflow is scheduled to run daily at 3:00 AM UTC. You can modify the cron expression in the workflow file to change this schedule.

```yaml
schedule:
  - cron: "0 3 * * *"  # UTC time
```

## 🔍 Design Principles

### Concurrency Management
- Uses `cancel-in-progress: false` to ensure running updates always complete
- The `os-update` concurrency group serializes update attempts properly

### Package Management Strategy
- `dist-upgrade` handles complex dependency changes and system upgrades
- `autoremove` automatically cleans up unused packages after updates

### Safety Measures
- Disk space verification requires 1GB minimum free space
- Error handling immediately terminates updates when issues arise
- Package operations use safe options for configuration handling

## 📊 Reporting

Each workflow run generates a summary report including:
- Update execution status
- Number of packages updated
- Disk space before and after updates
- Complete list of updated packages

## 🔄 Usage

### Manual Updates

1. Navigate to the "Actions" tab in your repository
2. Select the "OS Update" workflow
3. Click "Run workflow" and then "Run workflow" again to confirm

### Scheduled Updates

To enable scheduled updates:
1. Edit the workflow file and change `RUN_OS_UPDATE: "false"` to `RUN_OS_UPDATE: "true"`
2. Commit the change to your repository

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.
