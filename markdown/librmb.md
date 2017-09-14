<!-- .slide: data-state="section-break" id="section-break-4" data-timing="10s" -->
# Dovecot and Ceph


<!-- .slide: data-state="normal" id="librmb-dovecot" data-timing="20s" data-menu-title="Dovecot" -->
## Dovecot

<div>
    <img style="height: 25%; left: 40%; position: absolute" alt="CephFS"
         data-src="images/dovecot_logo.svg" />
</div>

### Open source project (LGPL 2.1, MIT) <!-- .element class="fragment" data-fragment-index="0"-->

### 72% market share (openemailsurvey.org, 02/2017) <!-- .element class="fragment" data-fragment-index="1"-->

### Objectstore plugin available (obox) <!-- .element class="fragment" data-fragment-index="2"-->
* supports only REST APIs like S3/Swift <!-- .element class="fragment" data-fragment-index="2"-->
* not open source <!-- .element class="fragment" data-fragment-index="2"-->
* requires Dovecot Pro <!-- .element class="fragment" data-fragment-index="2"-->
* large impact on TCO <!-- .element class="fragment" data-fragment-index="2"-->


<!-- .slide: data-state="normal" id="dovecot-obox" data-timing="20s" data-menu-title="librmb" -->
## Dovecot Pro obox Plugin
<div>
     <img style="width:90%;" alt="obox architecture overview" 
          data-src="images/dovecot-obox-plugin-architecture-normal.svg" />
</div>


<!-- .slide: data-state="normal" id="librmb-DT" data-timing="20s" data-menu-title="DT's approach" -->
## DT's approach
<div>
     <img style="position: absolute; width:40%; left: 70%;" alt="Partner"
          data-src="images/partner.png" />
</div> <!-- .element class="fragment" data-fragment-index="4"-->

* no open source solution on the market <!-- .element class="fragment" data-fragment-index="0"-->
* closed source is no option <!-- .element class="fragment" data-fragment-index="1"-->
* develop / sponsor a solution <!-- .element class="fragment" data-fragment-index="2"-->
* open source it <!-- .element class="fragment" data-fragment-index="3"-->
* partner with: <!-- .element class="fragment" data-fragment-index="4"-->
  * `Wido den Hollander (42on.com)` for consulting <!-- .element class="fragment" data-fragment-index="4"-->
  * `Tallence AG` for development <!-- .element class="fragment" data-fragment-index="4"-->
  * `SUSE` for Ceph <!-- .element class="fragment" data-fragment-index="4"-->


<!-- .slide: data-state="normal" id="librmb-DT-1" data-timing="20s" data-menu-title="Ceph Dovecot Plugin" -->
## Ceph plugin for Dovecot
<div>
     <img style="width:30%; left: 65%; position: absolute" alt="Ceph Plugin basics"
          data-src="images/dovecot-plugin-simple.svg" />
</div>

### First Step: hybrid approach <!-- .element class="fragment" data-fragment-index="0"-->

### Emails <!-- .element class="fragment" data-fragment-index="1"-->
* Store in RADOS Cluster <!-- .element class="fragment" data-fragment-index="1"-->

### Metadata and indexes <!-- .element class="fragment" data-fragment-index="2"-->
* Store in CephFS <!-- .element class="fragment" data-fragment-index="2"-->

### Be as generic as possible <!-- .element class="fragment" data-fragment-index="3"-->
* Split out code into libraries <!-- .element class="fragment" data-fragment-index="3"-->
* Integrate into corresponding upstream projects <!-- .element class="fragment" data-fragment-index="3"-->


<!-- .slide: data-state="normal" id="librmb-DT-2.0" data-timing="20s" data-menu-title="librmb" -->
## Librados mailbox (librmb)

<span class="fragment" data-fragment-index="0">
### Generic email abstraction on top of librados <!-- .element: class="fragment" data-fragment-index="0" -->
</span>

### Out of scope: <!-- .element: class="fragment" data-fragment-index="1" -->

<span class="fragment" data-fragment-index="2">
* User data and credential storage <!-- .element: class="fragment" data-fragment-index="2" -->
  * target are huge installations where usually are already solutions in place <!-- .element: class="fragment" data-fragment-index="2" -->
</span>

<span class="fragment" data-fragment-index="3">
* Full text indexes <!-- .element: class="fragment" data-fragment-index="3" -->
  * There are solutions already available and working outside email storage <!-- .element: class="fragment" data-fragment-index="3" -->
</span>


<!-- .slide: data-state="normal" id="librmb-DT-2.1" data-timing="20s" data-menu-title="librmb" -->
## Librados mailbox (librmb)

<div>
     <img alt="librmb architecture overview"
          data-src="images/dovecot-plugin-architecture-normal.svg" />
</div>


<!-- .slide: data-state="normal" id="librmb-DT-2.2" data-timing="20s" data-menu-title="librmb - Mail Object Format" -->
## librmb - Mail Object Format

### Mails are immutable regarding the RFC-5322 content <!-- .element: class="fragment" data-fragment-index="1" -->

### RFC-5322 content stored in RADOS directly <!-- .element: class="fragment" data-fragment-index="2" -->

<span class="fragment" data-fragment-index="3">
### Immutable attributes used by Dovecot stored in RADOS xattr <!-- .element: class="fragment" data-fragment-index="3" -->
* rbox format version <!-- .element: class="fragment" data-fragment-index="3" -->
* GUID <!-- .element: class="fragment" data-fragment-index="3" -->
* Received and save date <!-- .element: class="fragment" data-fragment-index="3" -->
* POP3 UIDL and POP3 order <!-- .element: class="fragment" data-fragment-index="3" -->
* Mailbox GUID <!-- .element: class="fragment" data-fragment-index="3" -->
* Physical and virtual size <!-- .element: class="fragment" data-fragment-index="3" -->
* Mail UID <!-- .element: class="fragment" data-fragment-index="3" -->
</span>

### writable attributes are stored in Dovecot index files <!-- .element: class="fragment" data-fragment-index="4" -->


<!-- .slide: data-state="normal" id="librmb-DT-2.3" data-timing="20s" data-menu-title="rmb tool" -->
## Dump email details from RADOS

<pre><code class="none">$> rmb -p mail_storage -N t1 ls M=ad54230e65b49a59381100009c60b9f7

mailbox_count: 1

MAILBOX: M(mailbox_guid)=ad54230e65b49a59381100009c60b9f7
         mail_total=2, mails_displayed=2
         mailbox_size=5539 bytes

         MAIL:   U(uid)=4
                 oid = a2d69f2868b49a596a1d00009c60b9f7
                 R(receive_time)=Tue Jan 14 00:18:11 2003
                 S(save_time)=Mon Aug 21 12:22:32 2017
                 Z(phy_size)=2919 V(v_size) = 2919 stat_size=2919
                 M(mailbox_guid)=ad54230e65b49a59381100009c60b9f7
                 G(mail_guid)=a3d69f2868b49a596a1d00009c60b9f7
                 I(rbox_version): 0.1
[..]
</code></pre>


<!-- .slide: data-state="normal" id="librmb-DT-2.4" data-timing="20s" data-menu-title="rados-dict" -->
## RADOS Dictionary Plugin

### make use of Ceph omap key/value store
### RADOS namespaces
 * `shared/<key>`
 * `priv/<key>`

### used by Dovecot to store metadata, quota, ...


<!-- .slide: data-state="normal" id="librmb-DT-3" data-timing="20s" data-menu-title="librmb" -->
## It's open source!

### <span>License: `LGPLv2.1`</span><!-- .element: class="fragment" data-fragment-index="0" -->

### <span>Language: `C++`</span> <!-- .element: class="fragment" data-fragment-index="1" -->

### <span>Location: <a href="https://github.com/ceph-dovecot/">github.com/ceph-dovecot/</a></span> <!-- .element: class="fragment" data-fragment-index="2" -->

<span class="fragment" data-fragment-index="3">
### Supported Dovecot versions: <!-- .element: class="fragment" data-fragment-index="3" -->
* 2.2 >= 2.2.21 <!-- .element: class="fragment" data-fragment-index="3" -->
* 2.3 <!-- .element: class="fragment" data-fragment-index="3" -->
</span>


<!-- .slide: data-state="normal" id="ceph-requirements" data-timing="20s" data-menu-title="Ceph requirements" -->
## Ceph Requirements

<span class="fragment" data-fragment-index="0">
### Performance <!-- .element: class="fragment" data-fragment-index="0" -->
* Write performance for emails is critical <!-- .element: class="fragment" data-fragment-index="0" -->
* metadata/index read/write performance <!-- .element: class="fragment" data-fragment-index="0" -->
</span>

<span class="fragment" data-fragment-index="1">
### Cost <!-- .element: class="fragment" data-fragment-index="1" -->
* Erasure Coding (EC) for emails <!-- .element: class="fragment" data-fragment-index="1" -->
* Replication for CephFS <!-- .element: class="fragment" data-fragment-index="1" -->
</span>

<span class="fragment" data-fragment-index="2">
### Reliability <!-- .element: class="fragment" data-fragment-index="2" -->
* MUST survice failure of disk, server, rack and even fire compartments <!-- .element: class="fragment" data-fragment-index="2" -->
</span>


<!-- .slide: data-state="normal" id="ceph-version" data-timing="20s" data-menu-title="Ceph version" -->
## Which Ceph Release?

<div>
     <img style="width: 55%; left: 50%; position: absolute" alt="ceph luminous"
          data-src="images/ceph-luminous.png" />
</div> <!-- .element: class="fragment" data-fragment-index="4" -->

### Required Features: <!-- .element: class="fragment" data-fragment-index="0" -->

* <!-- .element: class="fragment" data-fragment-index="1" --> Bluestore
  * <!-- .element: class="fragment" data-fragment-index="1" --> should be at least 2x faster than filestore
* <!-- .element: class="fragment" data-fragment-index="2" --> CephFS
  * <!-- .element: class="fragment" data-fragment-index="2" --> Stable release
  * <!-- .element: class="fragment" data-fragment-index="2" --> Multi-MDS
* <!-- .element: class="fragment" data-fragment-index="3" --> Erasure coding


<!-- .slide: data-state="normal" id="ceph-suse" data-timing="20s" data-menu-title="SUSE Products" -->
## SUSE Products to use

### SLES 12-SP3 and SES 5
<div>
     <img style="width: 80%;" alt="ceph luminous"
          data-src="images/SUSE_Products.png" />
</div>
