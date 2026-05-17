# GIF-to-mp4-Bulk
Bulk convert GIF animations into mp4 videos to save huge amount of space on disk.


### 🟦 Windows (PowerShell)
Navigate to the directory containing your `.gif` files, hold `Shift`, right-click an empty area, and select **Open PowerShell window here**. Paste and run the following block:

```powershell
# 1. Install FFmpeg via winget if it isn't already installed
if (-not (Get-Command ffmpeg -ErrorAction SilentlyContinue)) {
    Write-Host "FFmpeg not detected. Installing via winget..." -ForegroundColor Cyan
    winget install "FFmpeg (Essentials Build)" --silent
    Write-Host "Installation initiated. Please restart PowerShell and rerun this script." -ForegroundColor Yellow
    exit
}

# 2. Execute bulk conversion loop
Get-ChildItem *.gif | ForEach-Object {
    $outputName = $_.BaseName + ".mp4"
    ffmpeg -i $_.Name -movflags faststart -pix_fmt yuv420p -vf "scale=trunc(iw/2)*2:trunc(ih/2)*2" -b:v 2M $outputName -y
}


### For Linux / macOS (Bash)

Open your terminal, navigate to your directory containing the GIFs, and run this loop:
Bash

# Ensure ffmpeg is installed (Debian/Ubuntu: sudo apt install ffmpeg)
for file in *.gif; do
    [ -e "$file" ] || continue
    ffmpeg -i "$file" -movflags faststart -pix_fmt yuv420p -vf "scale=trunc(iw/2)*2:trunc(ih/2)*2" -b:v 2M "${file%.gif}.mp4" -y
done





This work is licensed under:
Creative Commons Non-Commercial (CC BY-NC 4.0)
