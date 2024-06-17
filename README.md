# Rename and Move Files Script

This repository contains a script for renaming and moving files on a remote server. The script is designed to rename all files in a specified directory that match a given pattern. The files are renamed sequentially starting from a specified number and are moved to a new directory.

## Overview

The script connects to a remote server via SSH, renames files that match the pattern `3gpp_3D_UMA_NLOS_M_512_velo500*.mat`, and moves them to a new directory named `changedfiles`. The renaming starts from a specified index and increments sequentially.

## Usage

### Prerequisites

- Ensure you have SSH access to the remote server.
- Make sure the necessary directories exist on the remote server or let the script create them.
- Handle SSH key authentication to avoid password prompts during script execution.

### Instructions

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/your-username/your-repository.git
   cd your-repository

#Script Details
bash
#Copy code

```
#!/bin/bash

# Script Name: rename_and_move_files.sh
# Description: This script renames all files in a remote server directory that match the pattern 
#              "3gpp_3D_UMA_NLOS_M_512_velo500*.mat". The files are renamed sequentially starting 
#              from a specified number and are moved to a new directory called "changedfiles".
# Usage: ./rename_and_move_files.sh
# Author: Your Name
# Date: YYYY-MM-DD

# Define SSH connection parameters
remoteUser="admins"                              # Username for SSH connection
remoteHost="10.171.9.236"                        # Hostname or IP address of the remote server
remoteFolderPath="/home/admins/CP-OFDM_OTFS_5G_turbo/sftp1/3GPPChannelModels"  # Path to the target directory on the remote server
changedFilesFolderPath="${remoteFolderPath}/changedfiles"  # Path to the directory for renamed files

# Define starting number for renaming
startRenameIndex=45205  # Starting index for the new file names

# SSH command to execute the renaming and moving on the remote server
ssh ${remoteUser}@${remoteHost} <<EOF
    # Define variables inside the SSH session
    remoteFolderPath="${remoteFolderPath}"
    changedFilesFolderPath="${changedFilesFolderPath}"
    startRenameIndex=${startRenameIndex}

    # Create the changedfiles directory if it doesn't exist
    mkdir -p "\${changedFilesFolderPath}"

    # Initialize the counter for renaming
    count=\${startRenameIndex}

    # Loop through files matching the pattern
    cd "\${remoteFolderPath}"
    for file in 3gpp_3D_UMA_NLOS_M_512_velo500*.mat; do
        # Define the new file name
        newFileName="3gpp_3D_UMA_NLOS_M_512_velo500_\${count}.mat"
        
        # Log the renaming action
        echo "Renaming \${file} to \${newFileName}"
        
        # Move and rename the file
        mv "\${file}" "\${changedFilesFolderPath}/\${newFileName}"
        
        # Increment the counter
        ((count++))
    done
EOF

# Log completion message
echo "File renaming and moving completed."
```

Save the Script:
Save the script as rename_and_move_files.sh in the cloned repository directory.

#Make the Script Executable:

bash
#Copy code
```chmod +x rename_and_move_files.sh ```
Execute the Script:

bash
#Copy code
```./rename_and_move_files.sh```
#Notes
Make sure to update the remoteUser, remoteHost, remoteFolderPath, and startRenameIndex variables in the script as per your requirements.
The script uses SSH to connect to the remote server and perform file operations. Ensure that your SSH keys are properly configured to avoid password prompts.
This script assumes that the files to be renamed are in the format 3gpp_3D_UMA_NLOS_M_512_velo500*.mat.


This README.md file provides a comprehensive overview, usage instructions, and the script i
