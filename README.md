<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>


# osTicket- Prerequisites and Installation Tutorial

This tutorial guides you through the steps to create a Windows 10 Virtual Machine in Azure and install osTicket with all necessary dependencies.

## Environments and Technologies Used:
- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)

## Operating Systems Used:
- Windows 10</b> (22H2)
  
## Prerequisites

Before you begin, ensure you have the following:

1. **Azure Account**: You need an active Azure subscription to create and manage resources.
2. **Remote Desktop Client**: To connect to the Windows VM in Azure.
3. **osTicket Installation Files**: Download from [Google Drive](https://drive.google.com/drive/u/1/folders/1APMfNyfNzcxZC6EzdaNfdZsUwxWYChf6).


## Table of Contents
- [Part 1: Create Virtual Machine in Azure](#part-1-create-virtual-machine-in-azure)
- [Part 2: Installation](#part-2-installation)
- [Clean Up](#clean-up)
- [Notes](#notes)

## Part 1: Create Virtual Machine in Azure

1. **Create a Resource Group in Azure**

2. **Create a Windows 10 Virtual Machine (VM)**
   - Use 2-4 Virtual CPUs.
   - Allow it to create a new Virtual Network (Vnet).

## Part 2: Installation

1. **Create an Azure Virtual Machine Windows 10, 4 vCPUs**
   - **Name**: `Vm-osticket`
   - **Username**: `labuser` (example)
   - **Password**: `osTicketPassword1!` (example)

2. **Download Installation Files**
   - [osTicket Installation Files](https://drive.google.com/drive/u/1/folders/1APMfNyfNzcxZC6EzdaNfdZsUwxWYChf6)

3. **Install / Enable IIS in Windows with the following features**:
   - **CGI and Common HTTP Features**
   - **World Wide Web Services -> Application Development Features ->**
     - [X] CGI
     - [X] Common HTTP Features
   - **Internet Information Services -> Web Management Tools -> IIS Management Console**
     - [X] IIS Management Console

4. **From the Installation Files, download and install the following**:
   - **PHP Manager for IIS**: `PHPManagerForIIS_V1.5.0.msi`
   - **Rewrite Module**: `rewrite_amd64_en-US.msi`

5. **Create the directory `C:\PHP`**

6. **Download and install PHP 7.3.8**:
   - **File**: `php-7.3.8-nts-Win32-VC15-x86.zip`
   - **Unzip** the contents into `C:\PHP`

7. **Download and install VC_redist.x86.exe**

8. **Download and install MySQL 5.5.62**:
   - **File**: `mysql-5.5.62-win32.msi`
   - **Typical Setup**
   - **Launch Configuration Wizard (after install) ->**
   - **Standard Configuration**
   - **Password**: `Password1`

9. **Open IIS as an Admin**

10. **Register PHP from within IIS**

11. **Reload IIS (Open IIS, Stop and Start the server)**

12. **Install osTicket v1.15.8**:
    - Download osTicket from the Installation Files Folder.
    - Extract and copy the “upload” folder to `C:\inetpub\wwwroot`.
    - Within `C:\inetpub\wwwroot`, rename “upload” to “osTicket”.

13. **Reload IIS (Open IIS, Stop and Start the server)**

14. **Go to sites -> Default -> osTicket**:
    - On the right, click “Browse *:80”.

15. **Enable PHP Extensions**:
    - **Back to IIS, sites -> Default -> osTicket**
    - Double-click PHP Manager.
    - Click “Enable or disable an extension”.
    - Enable: `php_imap.dll`, `php_intl.dll`, `php_opcache.dll`.
    - Refresh the osTicket site in your browser and observe the changes.

16. **Rename `ost-config.php`**:
    - From: `C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php`
    - To: `C:\inetpub\wwwroot\osTicket\include\ost-config.php`

17. **Assign Permissions to `ost-config.php`**:
    - Disable inheritance -> Remove All.
    - New Permissions -> Everyone -> All.

18. **Continue Setting up osTicket in the browser**:
    - **Name**: Helpdesk
    - **Default email**: (receives email from customers)

19. **Download and install HeidiSQL from the Installation Files**

20. **Open HeidiSQL**:
    - Create a new session, `root/Password1`.
    - Connect to the session.
    - Create a database called `osTicket`.

21. **Continue Setting up osTicket in the browser**:
    - **MySQL Database**: `osTicket`
    - **MySQL Username**: `root`
    - **MySQL Password**: `Password1`
    - Click “Install Now!”

22. **Congratulations!** 
    - Browse to your help desk login page: `http://localhost/osTicket/scp/login.php`

## Clean Up

1. **Delete**: `C:\inetpub\wwwroot\osTicket\setup`

2. **Set Permissions to “Read” only**: 
   - `C:\inetpub\wwwroot\osTicket\include\ost-config.php`

## Notes

- Browse to your help desk login page: `http://localhost/osTicket/scp/login.php`
- End Users osTicket URL: `http://localhost/osTicket/`

  That's the end of this tutorial.
