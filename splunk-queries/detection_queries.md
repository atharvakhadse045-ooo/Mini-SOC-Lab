# Splunk SPL Queries — Mini SOC Lab

## Detect Failed SSH Login Attempts
source="/var/log/auth.log" "Failed password"

## Count Failed Attempts by Host
source="/var/log/auth.log" "Failed password" | stats count by host

## Attack Timeline Visualization
source="/var/log/auth.log" "Failed password" | timechart count by host

## Identify Source IP of Attacker
source="/var/log/auth.log" "Failed password" | rex "from (?<src_ip>\d+\.\d+\.\d+\.\d+)" | stats count by src_ip

## Check for Successful Logins After Failed Attempts
source="/var/log/auth.log" ("Failed password" OR "Accepted password") | stats count by host