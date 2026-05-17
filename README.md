# GIF-to-mp4-Bulk
Bulk convert GIF animations into mp4 videos to save huge amount of space on disk.


For Windows (PowerShell)

Open the folder containing your GIFs, hold Shift, right-click an empty space, and select Open PowerShell window here. Paste this script and hit Enter:
PowerShell

# Install FFmpeg via winget if you don't have it already
if (-not (Get-Command ffmpeg -ErrorAction SilentlyContinue)) {
    winget install "FFmpeg (Essentials Build)" --silent
    Write-Host "Please restart PowerShell for FFmpeg to take effect, then rerun the script." -ForegroundColor Yellow
    exit
}

# Run the bulk conversion
Get-ChildItem *.gif | ForEach-Object {
    $outputName = $_.BaseName + ".mp4"
    ffmpeg -i $_.Name -movflags faststart -pix_fmt yuv420p -vf "scale=trunc(iw/2)*2:trunc(ih/2)*2" -b:v 2M $outputName -y
}

For Linux / macOS (Bash)

Open your terminal, navigate to your directory containing the GIFs, and run this loop:
Bash

# Ensure ffmpeg is installed (Debian/Ubuntu: sudo apt install ffmpeg)
for file in *.gif; do
    [ -e "$file" ] || continue
    ffmpeg -i "$file" -movflags faststart -pix_fmt yuv420p -vf "scale=trunc(iw/2)*2:trunc(ih/2)*2" -b:v 2M "${file%.gif}.mp4" -y
done





This work is licensed under:
Creative Commons Non-Commercial (CC BY-NC 4.0)
