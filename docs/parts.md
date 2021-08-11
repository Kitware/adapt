#  Payload Bill of Materials

* Embedded Computer with GPU ($750 \*):
    [Nvidia Jetson Xavier AGX](https://developer.nvidia.com/embedded/jetson-agx-xavier-developer-kit)
* Color Camera option 1 (global shutter):
    - Global shutter ($1750): [FLIR Blackfly S GigE BFS-PGE-161S7C-C](https://www.flir.com/products/blackfly-s-gige/?model=BFS-PGE-161S7C-C)
    - Lens ($1078): [Edmund Optics #86-569](https://www.edmundoptics.com/p/8mm-focal-length-hp-series-fixed-focal-length-lens/41693/)
* Color Camera option 2 (rolling shutter \*\*):
    - Rolling shutter ($780): [FLIR Blackfly S GigE BFS-PGE-200S6C-C](https://www.flir.com/products/blackfly-s-gige/?model=BFS-PGE-200S6C-C)
    - Lens ($550): [Computar V0826-MPZ](https://computar.com/product/1449/V0826-MPZ)
* Inertial Navigation System ($3230):
    [Advanced Navigation Spatial](https://www.advancednavigation.com/products/spatial)
* Wireless communications:
    - On payload ($182): [airMAX Bullet AC Dual-Band IP67 Radio](https://store.ui.com/collections/operator-airmax-devices/products/bullet-ac-ip67-1)
    - Antenna on payload ($15): [N-Type Dual Band](https://www.trendnet.com/products/wireless/5-7dBi-Outdoor-Dual-Band-Omni-Antenna-Kit-TEW-AO57)
    - Bridge at Base station ($80): [Ubiquiti LBE-5AC-GEN2-US LiteBeam Wireless](https://www.ui.com/airmax/litebeam-ac-gen2/)
* Other Required components:
    - M.2 NVMe SSD 1TB ($150): [Samsung 970 EVO](https://www.samsung.com/us/computing/memory-storage/solid-state-drives/ssd-970-evo-nvme-m-2-1tb-mz-v7e1t0bw/)
    - PoE injector for wireless ($8): [Passive single port injector](https://shop.poetexas.com/products/gpoe-1-wm)
    - PCIe Network card ($27): [STARTECH 1-PORT PCI EXPRSS GIGABIT](https://www.startech.com/en-us/networking-io/st1000spex2)
    - Cable for camera power ($67): [6-pin GPIO Hirose Connector](https://www.edmundoptics.com/p/blackflyreg-6-pin-gpio-hirose-connector-45m-cable/30350/)
    - Carbon fiber frame ($500): (Custom - Open Hardware CAD files to be uploaded)
* Misc:
    - Antenna adapter ($5): N Female to N Female
    - Level converter ($18): [Bi-Directional Level converter](https://www.sparkfun.com/products/12009)
    - (Mounting hardware)
    - (RJ45 Network cables)
    - (Misc. wiring and connectors)
    - (Misc. frame mounts, stand-offs, misc screws)

Total components Cost: $6574 - $8060

!!! note "Open Hardware"
    We will be updating this soon. In the spirit of Open Hardware, all the hardware components were selected from off-the-shelf components.

\* Approximate cost at time of purchase - some prices may vary (prices in USD including taxes and shipping)

\*\* The rolling shutter version of the camera is a cheaper option. However, it is not recommended if you intend to exploit the imagery for structure from motion (e.g., [TeleSculptor](https://telesculptor.org/)).
