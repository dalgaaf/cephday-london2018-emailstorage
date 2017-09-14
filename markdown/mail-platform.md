<!-- .slide: data-state="section-break" id="section-break-1" data-timing="10s" -->
# TelekomMail platform


<!-- .slide: data-state="normal" id="telekommail" data-timing="20s" data-menu-title="TelekomMail" -->
## TelekomMail

* DT's mail platform for customers
<!-- .element class="fragment" -->
* dovecot
<!-- .element class="fragment" -->
* Network-Attached Storage (NAS)
<!-- .element class="fragment" -->
* NFS (sharded)
<!-- .element class="fragment" -->
* ~1.3 petabyte net storage
<!-- .element class="fragment" -->
* ~39 million accounts
<!-- .element class="fragment" -->


<!-- .slide: data-state="normal" id="mailplatform-nfs" data-timing="20s" data-menu-title="NFS" -->
## NFS Operations

<center><img src="images/nfs-ops_libreoffice.png" style="width:100%"></center>


<!-- .slide: data-state="normal" id="mailplatform-nfs" data-timing="20s" data-menu-title="NFS" -->
## NFS Traffic

<center><img data-src="images/nfs-traffic_libreoffice.png" style="width:100%"></center>


<!-- .slide: data-state="normal" id="mailplatform-nfs-stats" data-timing="20s" data-menu-title="NFS-stats" -->
## NFS Statistics

### ~42% usable raw space

### NFS IOPS <!-- .element class="fragment" data-fragment-index="1"-->
  * max: ~835,000 <!-- .element class="fragment" data-fragment-index="1"-->
  * avg: ~390,000 <!-- .element class="fragment" data-fragment-index="1"-->

### relevant IO: <!-- .element class="fragment" data-fragment-index="2"-->
  * WRITE: 107,700 / 50,000 <!-- .element class="fragment" data-fragment-index="2"-->
  * READ:  65,700 / 30,900 <!-- .element class="fragment" data-fragment-index="2"-->


<!-- .slide: data-state="normal" id="mailplatform-mails-nums" data-timing="20s" data-menu-title="email statistics" -->
## Email Statistics

### 6.7 billion emails <!-- .element class="fragment" data-fragment-index="1"-->
  * 1.2 petabyte net <!-- .element class="fragment" data-fragment-index="1"-->
  * compression <!-- .element class="fragment" data-fragment-index="1"-->

### 1.2 billion index/cache/metadata files <!-- .element class="fragment" data-fragment-index="2"-->
  * avg: 24 kiB <!-- .element class="fragment" data-fragment-index="2"-->
  * max: ~600 MiB <!-- .element class="fragment" data-fragment-index="2"--> 


<!-- .slide: data-state="normal" id="mailplatform-mails-dist" data-timing="20s" data-menu-title="email distribution" -->
## Email Distribution

<center><img src="images/email-size-distribution_libreoffice.png" style="width:85%"></center>


<!-- .slide: data-state="normal" id="store-emails" data-timing="20s" data-menu-title="How stored?" -->
## How are emails stored?

### Emails are written once, read many (WORM) <!-- .element class="fragment" data-fragment-index="1"-->

### Usage depends on: <!-- .element class="fragment" data-fragment-index="2"-->
  * protocol (IMAP vs POP3) <!-- .element class="fragment" data-fragment-index="2"-->
  * user frontend (mailer vs webmailer) <!-- .element class="fragment" data-fragment-index="2"-->

### usually separated metadata, caches and indexes <!-- .element class="fragment" data-fragment-index="3"-->
  * lost of metadata/indexes is critical <!-- .element class="fragment" data-fragment-index="3"-->

### without attachments easy to compress <!-- .element class="fragment" data-fragment-index="4"-->


<!-- .slide: data-state="normal" id="store-emails-1" data-timing="20s" data-menu-title="Where to store emails?" -->
## Where to store emails?

### Filesystem <!-- .element class="fragment" data-fragment-index="1"-->
  * maildir <!-- .element class="fragment" data-fragment-index="1"-->
  * mailbox <!-- .element class="fragment" data-fragment-index="1"-->

### Database <!-- .element class="fragment" data-fragment-index="2"-->
  * SQL <!-- .element class="fragment" data-fragment-index="2"-->

### Objectstore <!-- .element class="fragment" data-fragment-index="3"-->
  * S3 <!-- .element class="fragment" data-fragment-index="3"-->
  * Swift <!-- .element class="fragment" data-fragment-index="3"-->

