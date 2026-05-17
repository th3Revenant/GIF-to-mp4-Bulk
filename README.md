# GIF-to-mp4-Bulk
Automated bulk convertion of GIF animations into mp4 videos to save huge amount of space on disk.


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
```

### 🟩 Linux & macOS (Bash)

Open your terminal, navigate (cd) to the folder containing your GIFs, and run the following script:
```Bash

# Ensure ffmpeg is installed beforehand:
# Debian/Ubuntu: sudo apt install ffmpeg
# macOS: brew install ffmpeg

for file in *.gif; do
    # Prevent errors if no GIF files exist
    [ -e "$file" ] || continue
    
    output_name="${file%.gif}.mp4"
    ffmpeg -i "$file" -movflags faststart -pix_fmt yuv420p -vf "scale=trunc(iw/2)*2:trunc(ih/2)*2" -b:v 2M "$output_name" -y
done
```


This work is licensed under:
Creative Commons Non-Commercial (CC BY-NC 4.0)
