---
jupyter:
  colab:
  kernelspec:
    display_name: Python 3
    name: python3
  language_info:
    name: python
  nbformat: 4
  nbformat_minor: 0
---

::: {.cell .markdown id="N44WLnNn1gjd"}
# 2 - Working with remote servers {#2---working-with-remote-servers}

**git branch name:** jbrowser
:::

::: {.cell .markdown id="8t5OxUXc5VTc"}
## Theory \[2\]

-   \[0.4\] What are [computer
    ports](https://www.cloudflare.com/learning/network-layer/what-is-a-computer-port/)
    on a high level? How many ports are there on a typical computer?
-   \[0.4\] What is the difference between http, https, ssh, and other
    protocols? In what sense are they similar? Name default ports for
    several data transfer protocols.
-   \[0.4\] Explain briefly: (1) what is IP, (2) what IPs are called
    \'white\'/public, (3) and what happens when you enter \'google.com\'
    into the web browser.
-   \[0.4\] What is Nginx? How does it work on the high level? List
    several alternative web servers.
-   \[0.4\] What is SSH, and for what is it typically used? Explain two
    ways to authenticate in an SSH server in detail.
:::

::: {.cell .markdown id="F-tIOAhDjNpN"}
-   \[0.4\] What are [computer
    ports](https://www.cloudflare.com/learning/network-layer/what-is-a-computer-port/)
    on a high level? How many ports are there on a typical computer?
    Computer ports refer to specific channels through which data is
    transmitted between different devices or computer systems on a
    network. These ports are identified by unique numeric values (port
    numbers) that allow different types of data to be transmitted
    through them.

In total, there are 65536 available communication ports on a regular
computer, but most often only a small part of them is used. Some of the
most common ports and their functions:

Port 80 --- HTTP (Hypertext Transfer Protocol)

Port 443 --- HTTPS (Secure Hypertext Transfer Protocol)

Port 22 --- SSH (secure shell)

Port 21 --- FTP (File Transfer Protocol)

Port 25 --- SMTP (Simple Mail Transfer Protocol)

Port 53 --- DNS (Domain Name System)

Port 3389 --- RDP (Remote Desktop Protocol)

Port 23 --- Telnet (teletype network)

Port 554 --- RTSP (Real-time Streaming Protocol)

Port 110 --- POP3 (Post Office Protocol version 3)

-   \[0.4\] What is the difference between http, https, ssh, and other
    protocols? In what sense are they similar? Name default ports for
    several data transfer protocols. HTTP (Hypertext Transfer Protocol)
    is a protocol used to transfer data on the Internet. It is the basis
    of data transmission on the Internet and is used to send and receive
    data between a web browser and a web server.

HTTPS (Hypertext Transfer Protocol Secure) is a secure version of HTTP.
It uses a secure connection (SSL/TLS) to encrypt the data transmitted
between the web browser and the web server.

SSH (Secure Shell) is a network protocol used for secure communication
between two devices. It is usually used for remote access to and
management of servers, as well as for secure file transfer between
systems.

The difference between the protocols lies in encryption and specific
tasks, but they are similar in that they are designed to transmit
information.

Some examples include FTP (File Transfer Protocol) for file transfer,
SMTP (simple mail transfer protocol) for sending email, and POP (Post
Office protocol) for receiving email.

Default ports:

-   HTTP port 80

-   HTTPS port 443

-   SSH port 22

-   \[0.4\] Explain briefly: (1) what is IP, (2) what IPs are called
    \'white\'/public, (3) and what happens when you enter \'google.com\'
    into the web browser. IP is a unique numeric identifier of a device
    in a computer network (local or global) operating over the IP
    protocol.

Public IP addresses - Those that can be accessed via the Internet are
called \"white\" or public IP addresses. These IP addresses are assigned
to devices that are directly connected to the Internet, such as servers
and routers.

what happens when you enter \'google.com\' into the web
browse:`<br>`{=html} The browser sends a request to the Domain Name
Server (DNS) to convert the domain name to an IP address. The DNS server
responds with the IP address of the server hosting the website. The
browser sends a request to the server using the IP address. The server
responds by sending the HTML, CSS, and JavaScript files of the website
to the browser. The browser uses these files to visualize the website
and display it to the user.
:::

::: {.cell .markdown id="7ZGJaIRLjPXv"}
-   \[0.4\] What is Nginx? How does it work on the high level? List
    several alternative web servers. Nginx is an open source web server
    that is used to host websites and web applications.

At a high level, Nginx works by accepting incoming HTTP requests from
clients (for example, web browsers) and redirecting them to a designated
internal server. Then the internal server processes the request and
returns the corresponding response, which Nginx sends back to the
client.

Nginx can be used as a stand-alone web server or as a reverse proxy
server, where it is located in front of several internal servers and
distributes incoming requests between them.
:::

::: {.cell .markdown id="DMZBdPgBbu5X"}
Some alternative web servers: Apache, IIS (Internet Information
Services) and LiteSpeed.

-   \[0.4\] What is SSH, and for what is it typically used? Explain two
    ways to authenticate in an SSH server in detail. SSH (Secure Shell)
    is a network protocol that provides secure remote access to a
    computer or server through an unsecured network. It is usually used
    for remote access to and management of servers, as well as for
    secure file transfer between systems.

There are two main ways to authenticate to an SSH server:

1\) Password-based authentication: This is the most common
authentication method in SSH. It assumes that the user enters the
correct password to gain access to the server. The password is usually
stored in a file named \"authorized_keys\" on the server, which is
encrypted and accessible only to the server administrator.

2\) Public key authentication. This authentication method involves using
a pair of cryptographic keys --- a public key and a private key --- to
authenticate the user. The user\'s public key is stored on the server,
and the private key is stored on the user\'s local computer. When a user
tries to connect to the server, the server sends a request that can be
decrypted using the user\'s private key. If the decryption was
successful, the user is granted access to the server.

Both of these authentication methods are secure, but public key
authentication is generally considered more secure because it does not
depend on the user remembering a password that can be easily compromised
or forgotten.
:::

::: {.cell .markdown id="Kh5oUQSA5WxI"}
## Problem \[6.5\] {#problem-65}

A real-life situation that occurred to me several times over the years.

Imagine wrapping up a large bioinformatics project and wanting to share
raw data with your colleagues in a friendly and straightforward format.
The best option would be to use an online genome browser and host your
data remotely, so it is easily accessible by anyone with a valid link.
This is exactly what we will be doing here.

*Please consider doing this HW using Linux since setting up the SSH
client on Windows is painful, and I won\'t be able to help you.*
:::

::: {.cell .markdown id="6phPxd80OiLP"}
**Remote Server**:

-   \[2\] Create a new virtual machine in the Yandex/Mail/etc cloud
    (order at least 10GB of free disk space). Generate SSH key pair and
    use it to connect to your server.
-   \[1\] Download the latest human genome assembly (GRCh38) from the
    Ensemble FTP server
    ([fasta](https://ftp.ensembl.org/pub/release-108/fasta/homo_sapiens/dna/Homo_sapiens.GRCh38.dna.primary_assembly.fa.gz),
    [GFF3](https://ftp.ensembl.org/pub/release-108/gff3/homo_sapiens/Homo_sapiens.GRCh38.108.gff3.gz)).
    Index the fasta using samtools (`samtools faidx`) and GFF3 using
    tabix.
-   \[1\] Select and download BED files for three ChIP-seq and one
    ATAC-seq experiment from the ENCODE (use one tissue/cell line).
    Sort, bgzip, and index them using tabix.

**JBrowse 2**

-   \[1\] Download and install [JBrowse 2](https://jbrowse.org/jb2/).
    Create a new jbrowse
    [repository](https://jbrowse.org/jb2/docs/cli/#jbrowse-create-localpath)
    in `/mnt/JBrowse/` (or some other folder).
-   \[0.25\] Install nginx and amend its config(/etc/nginx/nginx.conf)
    to contain the following section:

``` {.conf}
http {
  # Don't touch other options!
  # ........
  # ........

  # Comment this line(!):
  # include /etc/nginx/sites-enabled/*;

  # Add this:
  server {
    listen 80 default_server;
    index index.html;
    server_name _;

    location /jbrowse/ {
      alias /mnt/JBrowse/;	
    }
  }
}
```

-   \[0.25\] Restart the nginx (reload its config) and make sure that
    you can access the browser using a link like this:
    `http://64.129.58.13/jbrowse/`. Here `64.129.58.13` is your public
    IP address.
-   \[1\] Add your files (BED & FASTA & GFF3) to the genome browser and
    verify that everything works as intended. Don\'t forget to
    [index](https://jbrowse.org/jb2/docs/cli/#jbrowse-text-index) the
    genome annotation, so you could later search by gene names. Provide
    a [persistent
    link](https://jbrowse.org/jb2/docs/user_guides/basic_usage/#sharing-sessions)
    to a JBrowse 2 session with all your BED files and the genome
    annotation in the report (like
    [this](https://jbrowse.org/code/jb2/v2.3.1/?session=share-HShsEcnq3i&password=nYzTU)).
    *I must be able to access it without problems later.*

**Common mistakes**:

-   Using `/home/username` folder for JBrowse. Don\'t do this - you will
    have permission issues (403 forbidden) because by default home is
    only available to your user, not to the nginx user(group).
-   No trailing `/` in the config (`/jbrowse/`, `/mnt/JBrowse/`), or in
    the URL (`http://64.129.58.13/jbrowse/`).
-   If you have added tracks but they are not showing up in JBrowse -
    try reloading the page or use a private/incognito window.
-   Don\'t use `sudo` when using JBrowse CLI: (1) you risk messing up
    with permissions, (2) you don\'t really need it.
:::

::: {.cell .code id="pfbZiB0QPgzx"}
``` {.python}
sudo apt-get install wget 
sudo apt install gunzip samtools tabix

mkdir files
cd files

wget ftp://ftp.ensembl.org/pub/release-99/fasta/homo_sapiens/dna/Homo_sapiens.GRCh38.dna.primary_assembly.fa.gz

gunzip Homo_sapiens.GRCh38.dna.primary_assembly.fa.gz

samtools faidx Homo_sapiens.GRCh38.dna.primary_assembly.fa
```
:::

::: {.cell .code id="fjuKc-UhSuOy"}
``` {.python}
sudo apt-get install -y nginx
sudo nginx -s reload
sudo jbrowse create /vae/www/html/

sudo /home/alkirdeev/miniconda3/bin/jbrowse add-assembly Homo_sapiens.GRCh38.dna.primary_assembly.fa --type indexedFasta --load copy --out /var/www/html/jbrowse/

sudo /home/alkirdeev/miniconda3/bin/jbrowse text-index --file=/home/alkirdeev/genome_assembly/sorted.gff3.gz
```
:::

::: {.cell .code id="mRKeLqFtQWhs"}
``` {.python}
#Files from remote server
scp -r my_seq sveta2208@51.250.108.79:/home/sveta2208/files
```
:::

::: {.cell .code id="mbDj9nfJQgmo"}
``` {.python}
mkdir bed_files
cd bed_files

gunzip *.bed.gz

for file in ATAC FOXJ3 JUN POLR2A ; do sort -k1,1 -k2,2n $file > "sorted_$file"; done

bgzip sorted_*.bed

for file in sorted_*.bed.gz; do tabix -p bed $file;done

for i in ATAC FOXJ3 JUN POLR2A; do   gunzip sort_${i}.bed.gz;   awk '{gsub(/^chr/,""); print}' \
sort_${i}.bed > $(echo sort_${i}.bed| cut -d '.' -f 1)'_renamed.bed';   bgzip sort_${i}_renamed.bed;   tabix -f sort_${i}_renamed.bed.gz; done

for i in ATAC FOXJ3 JUN POLR2A 
do sudo jbrowse add-track sort_${i}_renamed.bed.gz --load copy --out /var/www/html/; done
```
:::

::: {.cell .markdown id="P3KW6yU8SxsF"}
## Server can be checked in <http://51.250.108.79/jbrowse/index.html> {#server-can-be-checked-in-http5125010879jbrowseindexhtml}
:::

::: {.cell .markdown id="apXcKkvn5a_O"}
## Extra points \[1.5\] {#extra-points-15}

-   \[1\] Create a Docker container for running JBrowse 2. It should be
    a self-contained application, listening on the default HTTP port.
    Users must be able to mount directories with custom configs and
    access them later without any problems.

Hint: to specify the config, use the config=PATH query parameter. E.g.
`http://64.129.58.13/jbrowse/?config=my_folder%2Fconfig.json` where
`my_folder%2Fconfig.json` is the
[escaped](https://en.wikipedia.org/wiki/Percent-encoding) path to the
config file.

-   \[0.5\] Give an in-depth explanation of the OSI model and how the
    TCP/IP stack works. Don\'t copy-paste descriptions from the
    internet; paraphrase and shorten as much as possible (imagine
    writing a cheat sheet for yourself).
:::

::: {.cell .markdown id="Gcaxh6CnZ2gK"}
*General:* The OSI model defines the structure of communication between
devices on the network, and the TCP/IP stack is a set of protocols that
implement this structure for communication over the Internet.

*More detailed* OSI It consists of 7 levels:

*Physical layer:* This layer is related to the physical transfer of data
between devices. This is about the types of cables and signals used to
transmit data.

*Data link layer:* Responsible for accurate data delivery between
devices that are connected directly, for example, between two computers
connected by a network cable. It performs error checking and flow
control to ensure correct data transmission.

*Network layer:* Responsible for routing data between devices that are
not directly connected. Determines the most efficient path for data.

*Transport layer:* Responsible for establishing, maintaining and
terminating connections between devices. It also provides flow control
and error checking to ensure correct data transmission.

*Session layer:* Responsible for establishing, maintaining and
terminating connections between applications on different devices. It
also manages the flow of data between applications.

*Presentation layer:* responsible for converting data into a form
understandable to the application layer. It handles tasks such as data
compression and encryption.

*Application layer:* The highest level of the OSI model responsible for
providing services to the user. It includes applications and programs
that allow users to interact with the network.

*TCP/IP* is a set of protocols that are used to transmit data over the
Internet. It is based on the OSI model and consists of 4 levels:

*Network Interface layer:* Corresponds to the physical layer and the
data link layer of the OSI model and is responsible for sending and
receiving data at the physical layer.

*Internet layer:* Corresponds to the network layer of the OSI model and
is responsible for routing data between devices.

*Transport layer:* Corresponds to the transport layer of the OSI model
and is responsible for establishing, maintaining and terminating
connections between devices.

*Application layer:* Corresponds to the session, presentation and
application layers of the OSI model and is responsible for providing
services to the user.
:::
