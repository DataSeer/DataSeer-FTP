# DataSeer-FTP

Documentation - How to send files to the DataSeer FTP server

## Table of Contents
- [FTP Server information](#ftp-server-information)
- [How to send files](#how-to-send-files)
  - [Using FileZilla](#using-filezilla)
  - [Using cURL](#using-curl)

## FTP Server information

- Hostname: ftp.dataseer.ai

## How to send files

### Using [Filezilla](https://filezilla-project.org/)

#### Preview

![image](https://github.com/user-attachments/assets/2aaa997b-f8f0-4dbb-9ca3-c12233646684)

#### More information

1. Enter the DataSeer FTP Hostname & your FTP login details
      * Host: ftp.dataseer.ai
      * Username: dataseer (replace it with your username)
      * Password: *******

2. Click on "Quickconnect"

_The following information should appear in the GUI_
```
Status:	Resolving address of dev.dataseer.ai
Status:	Connecting to xxx.xxx.xxx.xxx:21...
Status:	Connection established, waiting for welcome message...
Status:	Initializing TLS...
Status:	Verifying certificate...
Status:	TLS connection established.
Status:	Logged in
Status:	Retrieving directory listing...
Status:	Directory listing of "/" successful
```

3. Go to the desired folder (‘Remote Site’ section)
    * Folders can be created if necessary

For example, if I want to send files to an ‘upload’ folder :

_The following information should appear in the GUI_
```
Status:	Creating directory '/upload'...
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

---

### Using cURL

Files & folders can be uploaded to the DataSeer FTP server using the following cURL command line :

#### Preview

```
#------------------------------------------------------------------------------------------------
# Upload the file ‘/path/to/my/file.txt’ (‘Local Site’) to the ‘/upload/’ folder (‘Remote Site’).
#------------------------------------------------------------------------------------------------
# Replace USER & PASSWORD with your credentials
# Replace "/path/to/my/file.txt" with the path to be uploaded
#------------------------------------------------------------------------------------------------

curl --ssl-reqd --tlsv1.3 --insecure --user USER:PASSWORD -T "/path/to/my/file.txt" --ftp-pasv --progress-bar ftp://ftp.dataseer.ai:21/upload/
```

#### More information

| Argument | Description | Required |
|----------|-------------|----------|
| `--ssl-reqd --tlsv1.3 --insecure` | SSL/TLS arguments for secure connection | Yes |
| `--user USER:PASSWORD` | User credentials used for authentication | Yes |
| `-T "/path/to/my/file.txt"` | Path to the file to upload | Yes |
| `--ftp-pasv` | Enable FTP passive mode | Yes |
| `--progress-bar` | Display upload progress bar | No |
| `ftp://ftp.dataseer.ai:21/upload/` | FTP server address and target folder | Yes |
