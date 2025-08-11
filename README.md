

````markdown

\# Disk Space Report PowerShell Script



\## Overview

This project contains a PowerShell script that helps system administrators monitor disk space usage on multiple computers or servers.  

It collects the total and free disk space of all local drives and generates a report highlighting drives with low free space.



\## Features

\- Checks disk space on multiple remote computers.

\- Generates a CSV report with disk size, free space, and status.

\- Marks drives with free space less than a defined threshold as "LOW SPACE".

\- Easy to customize and extend.



\## Prerequisites

\- PowerShell 5.1 or higher (PowerShell 7.x recommended).

\- Remote PowerShell enabled on target computers (`Enable-PSRemoting -Force`).

\- Administrator access on remote computers.

\- List of target computers saved in a text file (`computers.txt`).



\## How to Use

1\. Edit `computers.txt` to include the hostnames or IP addresses of computers to check (one per line).  

2\. Open PowerShell and navigate to the project folder.  

3\. Run the script:  

&nbsp;  ```powershell

&nbsp;  .\\disk-report.ps1

````



4\. After execution, a CSV report file will be generated in the project folder with the current date and time in the filename.

5\. Open the CSV file with Excel or any text editor to review disk space status.



\## Customization



\* To change the low space threshold, edit the `$ThresholdGB` variable in the script (default is 10 GB).



\## Example Output



| ComputerName | Drive | Size(GB) | Free(GB) | Status    |

| ------------ | ----- | -------- | -------- | --------- |

| Server1      | C:    | 100      | 8.5      | LOW SPACE |

| Server2      | D:    | 200      | 50.3     | OK        |



\## License



This project is open-source and free to use.



---











