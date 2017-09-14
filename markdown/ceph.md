<!-- .slide: data-state="section-break" id="section-break-3" data-timing="10s" -->
# Ceph


<!-- .slide: data-state="normal" id="ceph-overview" data-timing="20s" data-menu-title="Ceph Components" -->
<center><img src="images/ceph-stack.svg" style="width:85%"></center>

NOTE: well known picture, short info on components


<!-- .slide: data-state="normal" id="motivation-goals" data-timing="20s" data-menu-title="Goals" -->
## Motivation

* Scale-out vs Scale-up
* Fast self healing
* Commodity hardware
* Prevent vendor lock-in
* Open Source where feasible
* Reduce Total Cost of Ownership (TCO)


<!-- .slide: data-state="normal" id="ceph-store-emails-1" data-timing="20s" data-menu-title="Ceph: Options" -->
## Ceph Options

### Filesystem <!-- .element class="fragment" data-fragment-index="1"-->
  * CephFS <!-- .element class="fragment" data-fragment-index="1"-->
  * NFS Gateway via RGW <!-- .element class="fragment" data-fragment-index="1"-->
  * Any filesystem on RBD <!-- .element class="fragment" data-fragment-index="1"-->

### Objectstore <!-- .element class="fragment" data-fragment-index="2"-->
  * S3/Swift via RGW <!-- .element class="fragment" data-fragment-index="2"-->
  * RADOS <!-- .element class="fragment" data-fragment-index="2"-->


<!-- .slide: data-state="normal" id="ceph-store-emails-2" data-timing="20s" data-menu-title="Ceph: Option CephFS" -->
## Where to store in Ceph?

<div>
    <img style="position: absolute; left: 30%;" alt="CephFS"
         data-src="images/cephfs.svg" />
</div>

### CephFS

* same issues as NFS <!-- .element class="fragment" -->
* mail storage on POSIX layer adds complexity <!-- .element class="fragment" -->
* no option for emails <!-- .element class="fragment" -->
* usable for metadata/caches/indexes <!-- .element class="fragment" -->
<br>
<br>
<br>


<!-- .slide: data-state="normal" id="ceph-store-emails-3" data-timing="20s" data-menu-title="Ceph: Option RBD" -->
## Where to store in Ceph?

<div>
    <img style="position: absolute; left: 30%;" alt="RBD"
         data-src="images/rbd.svg" />
</div>

### RBD

* needs sharding and large RBDs <!-- .element class="fragment" -->
* needs account migration <!-- .element class="fragment" -->
* needs RBD/fs extend scenarios <!-- .element class="fragment" -->
* no sharing between clients <!-- .element class="fragment" -->
* impracticable <!-- .element class="fragment" -->
<br>
<br>


<!-- .slide: data-state="normal" id="ceph-store-emails-4" data-timing="20s" data-menu-title="Ceph: Option RadosGW" -->
## Where to store in Ceph?

<div>
    <img style="position: absolute; left: 30%;" alt="RGW"
         data-src="images/rgw.svg" />
</div>

### RadosGW
* can store emails as objects <!-- .element class="fragment" -->
* extra network hops <!-- .element class="fragment" -->
* potential bottleneck <!-- .element class="fragment" -->
* very likely not fast enough <!-- .element class="fragment" -->
<br>
<br>
<br>


<!-- .slide: data-state="normal" id="ceph-store-emails-5" data-timing="20s" data-menu-title="Ceph: Option librados" -->
## Where to store in Ceph?

<div>
    <img style="position: absolute; left: 30%;" alt="librados"
         data-src="images/librados.svg" />
</div>

### Librados
* direct access to RADOS <!-- .element class="fragment" -->
* parallel I/O <!-- .element class="fragment" -->
* not optimized for emails <!-- .element class="fragment" -->
* how to handle metadata/caches/indexes? <!-- .element class="fragment" -->
<br>
<br>
<br>

