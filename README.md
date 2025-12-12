# Auto File Manager – Python Project

This project automatically organizes files based on their extensions.  
Place the script inside any folder and run it. The script will create category folders and move files into them.

## Features
- Automatically detects file types and organizes them.
- Creates category folders if they do not already exist.
- Supports Documents, Images, Videos, Audio, and Programming Files.
- Helps keep your folders clean and neatly arranged.

## How It Works
1. Place the Python script in the folder you want to organize.
2. Run the script using:
   python file_manager.py
3. The script will:
   - Scan all files in the folder
   - Identify the file type
   - Create necessary folders
   - Move files automatically

## Categories Included
- Documents (.pdf, .txt, .docx, .pptx, .odt)
- Images (.jpg, .png, .gif, .jpeg)
- Videos (.mp4, .avi, .mov, .flv, etc.)
- Audio (.mp3, .m4a, .wav, etc.)
- Programming Files (.py, .html, .css, .java, .cpp)
- Misc (for unsupported file types)

## Code Used
```
import os
from pathlib import Path

subcategory = {
    'DOCUMENTS': ['.pdf', '.txt', '.doc', 'rtf', '.pptx', '.docx', '.odt'],
    'AUDIO': ['.mp3', '.m4b', '.m4a', '.webvtt', '.cea-608/708', '.dfxp', '.sami',
              '.scc', '.srt', '.ttml', '.3gpp'],
    'VIDEOS': ['.mov', '.avi', '.mp4', '.3gp', '.ogg', '.oga', '.ogv', '.ogx',
               '.wmv', '.webm', '.flv', '.avi', '.QuickTime', '.hdv', '.mxf',
               '.mpeg-2', '.ts', '.wav', '.lfx', '.gfx', '.vob'],
    'IMAGES': ['.jpg', '.jpeg', '.raw', '.png', '.tiff', '.gif'],
    'PROGRAMMING FILES': ['.htm', '.html', '.cpp', '.c', '.py', '.css', '.java']
}

def findTheCategory(value):
    for category, ext_list in subcategory.items():
        for ext in ext_list:
            if ext == value:
                return category
    return 'MISC'

def organizeDir():
    for item in os.scandir():
        if item.is_dir():
            continue
        filePath = Path(item)
        fileType = filePath.suffix.lower()
        directory = findTheCategory(fileType)
        directoryPath = Path(directory)
        if not directoryPath.is_dir():
            directoryPath.mkdir()
        filePath.rename(directoryPath.joinpath(filePath))

organizeDir()
```

## Author
Aswini Kathirvel  
Python and SQL Enthusiast 
