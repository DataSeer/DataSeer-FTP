# DataSeer-FTP
Documentation - How to send files to the DataSeer FTP server

## FTP Server information

- Hostname: ftp.dataseer.ai

## How to send files

### Using [Filezilla](https://filezilla-project.org/)

#### Preview

![image](https://github.com/user-attachments/assets/884c7858-c321-4687-a8dd-3b6e37300007)


#### More information

1. Enter the DataSeer FTP Hostname & your FTP login details
      * Host: ftp.dataseer.ai
      * Username: dataseer (replace it with your username)
      * Password: *******

2. Click on "Quickconnect"

_The following information should appear in the GUI_
```
Status:	Resolving address of dev.dataseer.ai
Status:	Connecting to 139.162.174.64:21...
Status:	Connection established, waiting for welcome message...
Status:	Initializing TLS...
Status:	Verifying certificate...
Status:	TLS connection established.
Status:	Logged in
Status:	Retrieving directory listing...
Status:	Directory listing of "/" successful
```

3. Go to the desired folder (‘Remote Site’ section)
    * By default, an ‘upload’ folder is available
    * Folders can be created if necessary

_The following information should appear in the GUI_
```
Status:	Retrieving directory listing of "/upload"...
Status:	Directory listing of "/upload" successful
```

4. Select the files/folders you wish to send to DataSeer (‘Local Site’ section)
    * Drag & drop or double-click can be used to sent a file/folder
    * The files/folders sent will appear in the ‘Remote Site’ section

_The following information should appear in the GUI_
```
Status:	Starting upload of /home/user/test.txt
Status:	File transfer successful, transferred 6 B in 1 second
Status:	Retrieving directory listing of "/upload"...
Status:	Directory listing of "/upload" successful
```
