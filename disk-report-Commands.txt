# Server names List Path
$ComputerList = Get-Content ".\Server_List.txt"

# Free space threshold (in gigabytes)
$ThresholdGB = 10

# Array for storing results
$Report = @()

foreach ($Comp in $Server_List) {
    Write-Host "Checking $Comp ..." -ForegroundColor Cyan

    try {
        # Retrieving disk information (Local Drive)
        $disks = Get-WmiObject Win32_LogicalDisk -ComputerName $Comp -Filter "DriveType=3" -ErrorAction Stop

        foreach ($disk in $disks) {
            $FreeGB = [math]::Round($disk.FreeSpace / 1GB, 2)
            $SizeGB = [math]::Round($disk.Size / 1GB, 2)
            $Status = if ($FreeGB -lt $ThresholdGB) { "LOW SPACE" } else { "OK" }

            $Report += [PSCustomObject]@{
                ComputerName = $Comp
                Drive        = $disk.DeviceID
                'Size(GB)'   = $SizeGB
                'Free(GB)'   = $FreeGB
                Status       = $Status
            }
        }
    }
    catch {
        Write-Warning "Could not connect to $Comp. Error: $($_.Exception.Message)"
    }
}

# Saving log to a CSV file
$Date = Get-Date -Format "yyyy-MM-dd_HH-mm"
$ReportPath = ".\DiskReport_$Date.csv"
$Report | Export-Csv $ReportPath -NoTypeInformation

Write-Host "Report saved to $ReportPath" -ForegroundColor Green
