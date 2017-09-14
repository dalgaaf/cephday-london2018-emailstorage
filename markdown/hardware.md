<!-- .slide: data-state="section-break" id="section-break-5" data-timing="10s" -->
# Hardware


<!-- .slide: data-state="normal" id="hardware-0" data-timing="20s" data-menu-title="Hardware" -->
## Hardware

<div>
     <img style="position: absolute; width: 40%; left: 65%; " alt="librmb architecture overview"
          data-src="images/HPE-DL380Gen9.jpg" />
</div>

### Commodity x86_64 server <!-- .element: class="fragment" data-fragment-index="0" -->
* <!-- .element: class="fragment" data-fragment-index="1" --> HPE ProLiant DL380 Gen9
* <!-- .element: class="fragment" data-fragment-index="2" --> Dual socket
  * <!-- .element: class="fragment" data-fragment-index="2" --> Intel® Xeon® E5 V4
* <!-- .element: class="fragment" data-fragment-index="3" --> 2x Intel® X710-DA2 Dual-port 10G
* <!-- .element: class="fragment" data-fragment-index="4" --> 2x boot SSDs, SATA, HBA, no separate RAID controller

<br>
### CephFS, Rados, MDS and MON nodes <!-- .element: class="fragment" data-fragment-index="5" -->


<!-- .slide: data-state="normal" id="hardware-1" data-timing="20s" data-menu-title="Storage nodes" -->
## Storage Nodes

### CephFS SSD Nodes <!-- .element: class="fragment" data-fragment-index="0" -->
* <!-- .element: class="fragment" data-fragment-index="1" --> <b>CPU:</b> E5-2643v4 @ 3.4 GHz, 6 Cores, turbo 3.7GHz
* <!-- .element: class="fragment" data-fragment-index="1" --> <b>RAM:</b> 256 GByte, DDR4, ECC
* <!-- .element: class="fragment" data-fragment-index="1" --> <b>SSD:</b> 8x 1.6 TB SSD, 3 DWPD, SAS, RR/RW 125k/92k iops

### Rados HDD Nodes <!-- .element: class="fragment" data-fragment-index="2" -->
* <!-- .element: class="fragment" data-fragment-index="3" --> <b>CPU:</b> E5-2640v4 @ 2.4 GHz, 10 Cores, turbo 3.4GHz
* <!-- .element: class="fragment" data-fragment-index="3" --> <b>RAM:</b> 128 GByte, DDR4, ECC
* <!-- .element: class="fragment" data-fragment-index="3" --> <b>SSD:</b> 2x 400 GByte, 3 DWPD, SAS, RR/RW 108k/49k iops
  * <!-- .element: class="fragment" data-fragment-index="3" --> for BlueStore database etc.
* <!-- .element: class="fragment" data-fragment-index="3" --> <b>HDD:</b> 10x 4 TByte, 7.2K, 128 MB cache, SAS


<!-- .slide: data-state="normal" id="hardware-2" data-timing="20s" data-menu-title="Compute nodes" -->
## Compute Nodes

### MDS <!-- .element: class="fragment" data-fragment-index="0" -->
* <!-- .element: class="fragment" data-fragment-index="1" --> <b>CPU:</b> E5-2643v4 @ 3.4 GHz, 6 Cores, turbo 3.7GHz
* <!-- .element: class="fragment" data-fragment-index="1" --> <b>RAM:</b> 256 GByte, DDR4, ECC

<br>
### MON / SUSE admin <!-- .element: class="fragment" data-fragment-index="2" -->
* <!-- .element: class="fragment" data-fragment-index="3" --> <b>CPU:</b> E5-2640v4 @ 2.4 GHz, 10 Cores, turbo 3.4GHz
* <!-- .element: class="fragment" data-fragment-index="3" --> <b>RAM:</b> 64 GByte, DDR4, ECC


<!-- .slide: data-state="normal" id="hardware-3" data-timing="20s" data-menu-title="Hardware specs" -->
## Why this specific HW?

### Community recommendations? <!-- .element: class="fragment" data-fragment-index="0" -->
* <!-- .element: class="fragment" data-fragment-index="1" --> OSD: 1x 64-bit AMD-64, 1GB RAM/1TB of storage, 2x 1GBit NICs
* <!-- .element: class="fragment" data-fragment-index="2" --> MDS: 1x 64-bit AMD-64 quad-core, 1 GB RAM minimum per MDS, 2x 1GBit NICs

<br>
### NUMA, high clocked CPUs and large RAM overkill? <!-- .element: class="fragment" data-fragment-index="3" -->
* <!-- .element: class="fragment" data-fragment-index="4" --> Vendor did not offer single CPU nodes for number of drives
* <!-- .element: class="fragment" data-fragment-index="5" --> MDS performance is mostly CPU clock bound and partly single threaded
  * <!-- .element: class="fragment" data-fragment-index="5" --> High clocked CPUs for fast single threaded performance
* <!-- .element: class="fragment" data-fragment-index="6" --> Large RAM: better caching!

