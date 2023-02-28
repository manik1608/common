# Auto login in a web-page
Here are the steps to write a script that automatically logs in to your university's network after a certain period of time on Ubuntu:

1. Open a terminal window on your Ubuntu computer.
2. Type the following command to create a new file for your script:
    ```
    nano auto_login.sh
    ```
3. In the text editor that opens, type the following lines of code:
    ```
    #!/bin/bash
    while true
    do
        # Replace URL with the URL of the login page for your university's network
        wget -qO- URL | grep -q "login"
        if [ $? -eq 0 ]; then
        # Replace USERNAME and PASSWORD with your actual username and password
        wget --post-data 'username=USERNAME&password=PASSWORD' -qO- URL >/dev/null 2>&1
        echo "Logged in successfully."
        else
          echo "Already logged in."
        fi
        sleep 2400
    done
    ```
    Note: Replace "URL", "USERNAME", and "PASSWORD" with the actual URL, username, and password for your university's network.
4. Press "Ctrl + X" to exit the text editor, then type "Y" and press Enter to save the changes.
5. Type the following command to make the script executable:
    ```
    chmod +x auto_login.sh
    ```
6. Type the following command to run the script:
    ```
    ./auto_login.sh &
    ```
    The "&" at the end of the command will run the script in the background, so it will continue to run even after you close the terminal window.

The script will check every 2400 seconds (40 minutes) if you are logged in to your university's network. If you are not logged in, it will use the "wget" command to submit your username and password to the login page and log you in. If you are already logged in, it will do nothing. You can modify the sleep interval and the login credentials to suit your needs. Note that this script requires the "wget" command to be installed on your Ubuntu system. If it is not installed, you can install it by running the following command:
  ```
  sudo apt-get install wget
  ```
