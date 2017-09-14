<!-- .slide: data-state="section-break" id="section-break-6" data-timing="10s" -->
# Placement


<!-- .slide: data-state="normal" id="placement-1" data-timing="20s" data-menu-title="Placement issues" -->
## Issues

### Datacenter <!-- .element: class="fragment" data-fragment-index="0" -->
* <!-- .element: class="fragment" data-fragment-index="1" --> usually two independent fire compartments (FCs)
* <!-- .element: class="fragment" data-fragment-index="2" --> may additional virtual FCs

### Requirements <!-- .element: class="fragment" data-fragment-index="3" -->
* <!-- .element: class="fragment" data-fragment-index="4" --> Lost of customer data MUST be prevented
* <!-- .element: class="fragment" data-fragment-index="5" --> Any server, switch or rack can fail
* <!-- .element: class="fragment" data-fragment-index="5" --> One FC can fail
* <!-- .element: class="fragment" data-fragment-index="5" --> Data replication at least 3 times (or equivalent)


<!-- .slide: data-state="normal" id="placement-2" data-timing="20s" data-menu-title="Placement issues" -->
## Issues

### Questions
* <!-- .element: class="fragment" data-fragment-index="0" --> How to place 3 copies in two FCs?
* <!-- .element: class="fragment" data-fragment-index="1" --> How independent and reliable are the virtual FCs?
* <!-- .element: class="fragment" data-fragment-index="2" --> Network architecture?
* <!-- .element: class="fragment" data-fragment-index="3" --> Network bandwidth?


<!-- .slide: data-state="normal" id="placement-3" data-timing="20s" data-menu-title="3FCs" -->
<div>
  <center><img data-src="images/fc-ceph-EC+3xReplication-color.svg" style="width:95%"></center>
</div>


<!-- .slide: data-state="normal" id="placement-net-1" data-timing="20s" data-menu-title="Network" -->
## Network

### 10G network <!-- .element: class="fragment" data-fragment-index="0" -->
* <!-- .element: class="fragment" data-fragment-index="1" --> 2 NICs / 4 ports per node
* <!-- .element: class="fragment" data-fragment-index="1" --> SFP+ DAC

### Multi-chassis Link Aggregation (MC-LAG/M-LAG) <!-- .element: class="fragment" data-fragment-index="2" -->
* <!-- .element: class="fragment" data-fragment-index="2" --> For aggregation and fail-over

### Spine-Leaf architecture <!-- .element: class="fragment" data-fragment-index="3" -->
* <!-- .element: class="fragment" data-fragment-index="4" --> Interconnect must not reflect theoretical rack/FC bandwidth
* <!-- .element: class="fragment" data-fragment-index="5" --> L2: terminated in rack
* <!-- .element: class="fragment" data-fragment-index="6" --> L3: TOR <-> spine / spine <-> spine
* <!-- .element: class="fragment" data-fragment-index="7" --> Border Gateway Protocol (BGP)


<!-- .slide: data-state="normal" id="placement-net-2" data-timing="20s" data-menu-title="Network Overview" -->
<div>
  <center><img data-src="images/network-arch.svg" style="width:90%"></center>
</div>
