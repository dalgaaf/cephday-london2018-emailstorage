<!-- .slide: data-state="section-break" id="section-break-7" data-timing="10s" -->
# Next Steps


<!-- .slide: data-state="normal" id="status-2" data-timing="20s" data-menu-title="PoC" -->
## Proof-of-Concept

### Hardware <!-- .element: class="fragment" data-fragment-index="0" -->
* <!-- .element: class="fragment" data-fragment-index="1" --> 9 SSD nodes for CephFS
* <!-- .element: class="fragment" data-fragment-index="1" --> 12 HDD nodes
* <!-- .element: class="fragment" data-fragment-index="1" --> 3 MDS / 3 MON

### 2 FCs + 1 vFC <!-- .element: class="fragment" data-fragment-index="2" -->

### Testing <!-- .element: class="fragment" data-fragment-index="3" -->
* <!-- .element: class="fragment" data-fragment-index="4" --> run load tests
* <!-- .element: class="fragment" data-fragment-index="5" --> run failure scenarios against Ceph
* <!-- .element: class="fragment" data-fragment-index="6" --> improve and tune Ceph setup
* <!-- .element: class="fragment" data-fragment-index="7" --> verify and optimize hardware


<!-- .slide: data-state="normal" id="status-4" data-timing="20s" data-menu-title="Next Steps" -->
## Move to Production

### Production <!-- .element: class="fragment" data-fragment-index="0" -->
* <!-- .element: class="fragment" data-fragment-index="1" --> verify if all requirements are fulfilled
* <!-- .element: class="fragment" data-fragment-index="2" --> integrate in production
* <!-- .element: class="fragment" data-fragment-index="3" --> migrate users step-by-step
* <!-- .element: class="fragment" data-fragment-index="4" --> extend to final size
  * <!-- .element: class="fragment" data-fragment-index="4" --> 128 HDD nodes, 1200 OSDs, 4,7 PiB
  * <!-- .element: class="fragment" data-fragment-index="4" --> 15 SSD nodes, 120 OSDs, 175 TiB


<!-- .slide: data-state="normal" id="status-3" data-timing="20s" data-menu-title="Further Development" -->
## Further Development

### Goal: Pure RADOS backend, store metadata/index in Ceph omap

<div>
     <img style="width: 95%;" alt="librmb architecture overview"
          data-src="images/dovecot-plugin-architecture-pure-rados.svg" />
</div>
