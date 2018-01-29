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
* quite complex setup <!-- .element class="fragment" data-fragment-index="2"-->
* requires Dovecot Pro <!-- .element class="fragment" data-fragment-index="2"-->
* large impact on TCO <!-- .element class="fragment" data-fragment-index="2"-->


<!-- .slide: data-state="normal" id="librmb-DT" data-timing="20s" data-menu-title="DT's approach" -->
## DT's approach
<div>
     <img style="position: absolute; width:30%; left: 75%;" alt="Partner"
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
### First Step: hybrid approach <!-- .element class="fragment" data-fragment-index="0"-->

### Emails <!-- .element class="fragment" data-fragment-index="1"-->
* RADOS Cluster <!-- .element class="fragment" data-fragment-index="1"-->

### Metadata and indexes <!-- .element class="fragment" data-fragment-index="2"-->
* CephFS <!-- .element class="fragment" data-fragment-index="2"-->

### Generic email abstraction on top of librados <!-- .element class="fragment" data-fragment-index="4"-->
* Split code into libraries <!-- .element class="fragment" data-fragment-index="4"-->
* Integrate into corresponding upstream projects <!-- .element class="fragment" data-fragment-index="4"-->


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


<!-- .slide: data-state="normal" id="librmb-DT-2.4" data-timing="20s" data-menu-title="rados-dict" -->
## RADOS Dictionary Plugin

### make use of Ceph omap key/value store
### RADOS namespaces
 * `shared/<key>`
 * `priv/<key>`

### used by Dovecot to store metadata, quota, ...


<!-- .slide: data-state="normal" id="librmb-DT-3" data-timing="20s" data-menu-title="librmb" -->
## It's open source!

<div>
    <img style="position: absolute; width: 50%; left: 55%;" alt="Github Project Screenshot"
         data-src="images/github-ceph-dovecot_new.png" />
</div> <!-- .element: class="fragment" data-fragment-index="2" -->

### <span>License: `LGPLv2.1`</span><!-- .element: class="fragment" data-fragment-index="0" -->

### <span>Language: `C++`</span> <!-- .element: class="fragment" data-fragment-index="1" -->

### <span>Location: <a href="https://github.com/ceph-dovecot/">github.com/ceph-dovecot/</a></span> <!-- .element: class="fragment" data-fragment-index="2" -->

<span class="fragment" data-fragment-index="3">
### Supported Dovecot versions: <!-- .element: class="fragment" data-fragment-index="3" -->
* 2.2 >= 2.2.21 <!-- .element: class="fragment" data-fragment-index="3" -->
* 2.3 <!-- .element: class="fragment" data-fragment-index="3" -->
</span>

### still under development <!-- .element: class="fragment" data-fragment-index="4" -->

### <span>initial SLES12-SP3 and openSUSE RPMs: https://goo.gl/FymRhu</span> <!-- .element: class="fragment" data-fragment-index="5" -->


<!-- .slide: data-state="normal" id="ceph-version" data-timing="20s" data-menu-title="Ceph version" -->
## Which Ceph Release?

<div>
     <img style="width: 55%; left: 50%; position: absolute" alt="ceph luminous"
          data-src="images/ceph-luminous.png" />
</div> <!-- .element: class="fragment" data-fragment-index="5" -->

### Required Features: <!-- .element: class="fragment" data-fragment-index="0" -->

* <!-- .element: class="fragment" data-fragment-index="1" --> Bluestore
  * <!-- .element: class="fragment" data-fragment-index="1" --> write performance is critical
  * <!-- .element: class="fragment" data-fragment-index="1" --> should be at least 2x faster than filestore
* <!-- .element: class="fragment" data-fragment-index="2" --> CephFS
  * <!-- .element: class="fragment" data-fragment-index="2" --> Stable release
  * <!-- .element: class="fragment" data-fragment-index="2" --> Multi-MDS
* <!-- .element: class="fragment" data-fragment-index="3" --> Erasure coding
  * <!-- .element: class="fragment" data-fragment-index="3" --> Cost reduction
* <!-- .element: class="fragment" data-fragment-index="4" --> Resiliency, reliability and fault tolerance

### Enterprise products used: <!-- .element: class="fragment" data-fragment-index="6" -->
* <!-- .element: class="fragment" data-fragment-index="6" --> SES 5

