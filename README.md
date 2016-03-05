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
