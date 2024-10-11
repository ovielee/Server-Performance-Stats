# Server-Performance-Stats

https://roadmap.sh/projects/server-stats

Step 1: Install Required Packages
Make sure you have sysstat installed to use the mpstat command. Run:

```bash
sudo apt update
sudo apt install sysstat
```
Step 2: Create the Script File
Use a text editor to create the script file. You can use nano, vim, or any editor of your choice. Here, we'll use nano:

```bash
nano server-stats.sh
```
Step 3: Copy the Script
Copy the following script and paste it into the nano editor:
```bash
#!/bin/bash

# Function to calculate total CPU usage
function cpu_usage {
    echo "CPU Usage:"
    mpstat | awk '/Average/ {printf "%.2f%\n", 100 - $12}'
}

# Function to calculate total memory usage
function memory_usage {
    echo "Memory Usage:"
    free -h | awk 'NR==2{printf "Used: %s (%.2f%%)\nFree: %s\n", $3, $3*100/$2, $7}'
}

# Function to calculate total disk usage
function disk_usage {
    echo "Disk Usage:"
    df -h | awk '$NF=="/"{printf "Used: %s (%.2f%%)\nFree: %s\n", $3, $3*100/$2, $4}'
}

# Function to display top 5 processes by CPU usage
function top_cpu_processes {
    echo "Top 5 Processes by CPU Usage:"
    ps -eo pid,comm,%cpu --sort=-%cpu | head -n 6
}

# Function to display top 5 processes by memory usage
function top_memory_processes {
    echo "Top 5 Processes by Memory Usage:"
    ps -eo pid,comm,%mem --sort=-%mem | head -n 6
}

# Function to display additional stats
function additional_stats {
    echo "Additional Stats:"
    echo "OS Version: $(uname -a)"
    echo "Uptime: $(uptime -p)"
    echo "Load Average: $(cat /proc/loadavg | awk '{print $1, $2, $3}')"
    echo "Logged In Users: $(who | wc -l)"
    echo "Failed Login Attempts: $(grep 'Failed password' /var/log/auth.log | wc -l)"
}

# Main script execution
echo "=== Server Performance Stats ==="
cpu_usage
echo
memory_usage
echo
disk_usage
echo
top_cpu_processes
echo
top_memory_processes
echo
additional_stats
echo "==============================="

exit 0
#!/bin/bash

# Function to calculate total CPU usage
function cpu_usage {
    echo "CPU Usage:"
    mpstat | awk '/Average/ {printf "%.2f%\n", 100 - $12}'
}

# Function to calculate total memory usage
function memory_usage {
    echo "Memory Usage:"
    free -h | awk 'NR==2{printf "Used: %s (%.2f%%)\nFree: %s\n", $3, $3*100/$2, $7}'
}

# Function to calculate total disk usage
function disk_usage {
    echo "Disk Usage:"
    df -h | awk '$NF=="/"{printf "Used: %s (%.2f%%)\nFree: %s\n", $3, $3*100/$2, $4}'
}

# Function to display top 5 processes by CPU usage
function top_cpu_processes {
    echo "Top 5 Processes by CPU Usage:"
    ps -eo pid,comm,%cpu --sort=-%cpu | head -n 6
}

# Function to display top 5 processes by memory usage
function top_memory_processes {
    echo "Top 5 Processes by Memory Usage:"
    ps -eo pid,comm,%mem --sort=-%mem | head -n 6
}

# Function to display additional stats
function additional_stats {
    echo "Additional Stats:"
    echo "OS Version: $(uname -a)"
    echo "Uptime: $(uptime -p)"
    echo "Load Average: $(cat /proc/loadavg | awk '{print $1, $2, $3}')"
    echo "Logged In Users: $(who | wc -l)"
    echo "Failed Login Attempts: $(grep 'Failed password' /var/log/auth.log | wc -l)"
}

# Main script execution
echo "=== Server Performance Stats ==="
cpu_usage
echo
memory_usage
echo
disk_usage
echo
top_cpu_processes
echo
top_memory_processes
echo
additional_stats
echo "==============================="

exit 0
```
Step 4: Save and Exit
In nano, save the file by pressing CTRL + O, then press Enter. Exit by pressing CTRL + X.

Step 5: Make the Script Executable
Change the permissions of the script to make it executable:

```bash
chmod +x server-stats.sh
```
Step 7: Run the Script
Execute the script to see the server performance stats:
```bash
./server-stats.sh
```

Output of the Project
![image](https://github.com/user-attachments/assets/f170fafa-1ec0-4ea9-8981-40a7db32a7fd)





