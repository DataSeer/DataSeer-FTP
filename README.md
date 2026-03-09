# DataSeer-FTP

Documentation - How to send files to the DataSeer file server

## Table of Contents
- [Server information](#server-information)
- [Important: upload path differences](#important-upload-path-differences)
- [How to send files](#how-to-send-files)
  - [Using FileZilla](#using-filezilla)
  - [Using cURL](#using-curl)
  - [Using SFTP command line](#using-sftp-command-line)

## Server information

| | FTP / FTPS | SFTP |
|---|---|---|
| **Hostname** | ftp.dataseer.ai | ftp.dataseer.ai |
| **Port** | 21 | 22 |
| **Authentication** | Username + Password | Username + Password |

## Important: upload path differences

> **:warning: The upload path is different depending on the protocol used.**
>
> | Protocol | Upload path | Details |
> |----------|-------------|---------|
> | **FTP / FTPS** (port 21) | `/` | You land directly in the upload folder. Upload files at the root. |
> | **SFTP** (port 22) | `/upload` | You must navigate to `/upload` before uploading files. This directory may not be visible in some clients (e.g. FileZilla) but it exists and is **required**. |
>
> **Make sure the destination path is set to `/upload` when using SFTP.**

## How to send files

### Using [FileZilla](https://filezilla-project.org/)

#### Connection settings

1. Enter the DataSeer Hostname & your login details
      * Host: ftp.dataseer.ai
      * Username: *(your username)*
      * Password: *(your password)*
      * Port: **21** for FTP/FTPS or **22** for SFTP

2. Click on "Quickconnect"

#### FTP/FTPS connection (port 21)

_The following information should appear in the GUI_
```
Status:    Resolving address of ftp.dataseer.ai
Status:    Connecting to xxx.xxx.xxx.xxx:21...
Status:    Connection established, waiting for welcome message...
Status:    Initializing TLS...
Status:    Verifying certificate...
Status:    TLS connection established.
Status:    Logged in
Status:    Retrieving directory listing...
Status:    Directory listing of "/" successful
```

You land directly in the upload folder. You can upload files and create sub-folders here.

#### SFTP connection (port 22)

_The following information should appear in the GUI_
```
Status:    Connecting to ftp.dataseer.ai:22...
Status:    Connection established, waiting for welcome message...
Status:    Connected to ftp.dataseer.ai
Status:    Logged in
Status:    Retrieving directory listing...
Status:    Directory listing of "/" successful
```

> **:warning: With SFTP, you must navigate to the `/upload` directory before uploading files.** This directory may not be visible in the FileZilla directory listing — type `/upload` manually in the "Remote site" path bar and press Enter.

#### Uploading files

3. Navigate to the correct remote folder ('Remote Site' section)
    * **FTP/FTPS**: upload directly at the root `/`
    * **SFTP**: navigate to `/upload`
    * Sub-folders can be created if necessary

4. Select the files/folders you wish to send to DataSeer ('Local Site' section)
    * Drag & drop or double-click can be used to send a file/folder
    * The files/folders sent will appear in the 'Remote Site' section

_The following information should appear in the GUI_
```
Status:    Starting upload of /home/user/test.txt
Status:    File transfer successful, transferred 6 B in 1 second
```

---

### Using cURL

#### Upload via FTP/FTPS (port 21)

```bash
#------------------------------------------------------------------------------------------------
# Upload the file '/path/to/my/file.txt' to the root folder (which is the upload folder).
#------------------------------------------------------------------------------------------------
# Replace USER & PASSWORD with your credentials
# Replace "/path/to/my/file.txt" with the path to the file to upload
#------------------------------------------------------------------------------------------------

curl --ssl-reqd --tlsv1.3 --insecure --user USER:PASSWORD -T "/path/to/my/file.txt" --ftp-pasv --progress-bar ftp://ftp.dataseer.ai:21/
```

| Argument | Description | Required |
|----------|-------------|----------|
| `--ssl-reqd --tlsv1.3 --insecure` | SSL/TLS arguments for secure connection | Yes |
| `--user USER:PASSWORD` | User credentials used for authentication | Yes |
| `-T "/path/to/my/file.txt"` | Path to the file to upload | Yes |
| `--ftp-pasv` | Enable FTP passive mode | Yes |
| `--progress-bar` | Display upload progress bar | No |
| `ftp://ftp.dataseer.ai:21/` | FTP server address (root is the upload folder) | Yes |

#### Upload via SFTP (port 22)

> **:warning: With SFTP, you must specify `/upload/` as the destination path.**

```bash
#------------------------------------------------------------------------------------------------
# Upload the file '/path/to/my/file.txt' to the '/upload/' folder.
#------------------------------------------------------------------------------------------------
# Replace USER & PASSWORD with your credentials
# Replace "/path/to/my/file.txt" with the path to the file to upload
#------------------------------------------------------------------------------------------------

curl --insecure --user USER:PASSWORD -T "/path/to/my/file.txt" --progress-bar sftp://ftp.dataseer.ai:22/upload/
```

| Argument | Description | Required |
|----------|-------------|----------|
| `--insecure` | Skip host key verification (or use `--hostpubsha256` for strict verification) | Yes |
| `--user USER:PASSWORD` | User credentials used for authentication | Yes |
| `-T "/path/to/my/file.txt"` | Path to the file to upload | Yes |
| `--progress-bar` | Display upload progress bar | No |
| `sftp://ftp.dataseer.ai:22/upload/` | SFTP server address (**`/upload/` is required**) | Yes |

---

### Using SFTP command line

The `sftp` command is available on Linux and macOS.

> **:warning: With SFTP, you must upload files to the `/upload` directory.**

#### Interactive mode

```bash
sftp USER@ftp.dataseer.ai
```

Once connected:
```
cd /upload
put /path/to/my/file.txt
bye
```

#### Non-interactive mode (single file)

```bash
echo "put /path/to/my/file.txt /upload/file.txt" | sftp USER@ftp.dataseer.ai
```

#### Non-interactive mode (multiple files)

Create a batch file (e.g. `batch.sftp`):
```
cd /upload
put /path/to/my/file1.txt
put /path/to/my/file2.txt
bye
```

Then run:
```bash
sftp -b batch.sftp USER@ftp.dataseer.ai
```
