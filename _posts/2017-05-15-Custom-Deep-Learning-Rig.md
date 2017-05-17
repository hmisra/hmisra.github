---
layout: post
type: blog
title: Custom Deep Learning Rig
excerpt: Logs on building a fast GPU based Deep Learning Machine
comments: true
background: /hardware.jpg
published: true
authorname: Himanshu Misra
authordesignation: Data Scientist @ Legacy.com
authorimage: /himanshu.jpg
authorlinkedin: https://www.linkedin.com/in/hmisra
authorfacebook: https://www.facebook.com/himanshumisra1990
authorgithub: https://github.com/hmisra
authortwitter: https://twitter.com/himanshumisra
---


<div style="background-color: #F5f5f5;  padding: 50px;" >
<font size="3px" color="#999999" face="Helvetica" style="text-transform: uppercase; margin-bottom: 30px;">In Brief
</font> <br> 
<hr>


<li> Hardware Specifications </li>
<li> Build Logs </li>
<li> Getting up and Running </li>


</div>


## Introduction
----------------------------------
<br>

While finshing up my Udacity Deep Learning Nanodegree projects on my Macbook Pro with 2GB Nvidia Geforce GT 750 M I ended up exhausting all the GPU memory which started giving me out of memory exceptions for even a batch size of 16. This frustration combined with the some online research on cost effectiveness of custom build PC over Amazon P2 instances in long run made me invest some money in building this machine. Here are some helpful links which came up during my initial research. 

* [Tim Dettmers's](http://timdettmers.com/) blog is like a ray of light when you will find yourself lost in confusion of which component to select out of all myriad choices available in market. Do read all the blog posts to make an informed decision.

* I used [Andrej Karpathy's](https://twitter.com/karpathy?lang=en) build as a reference which he shared in his 2 year old tweet [here](https://pcpartpicker.com/user/badmephisto/saved/#view=mM3J7P)

* [PCPartPicker](https://pcpartpicker.com/) is a must use tool when you are building your own Computer. It can be used to decide your components, check reviews and ratings of each component, check compatibilities between them and find the best place to order them. In short its a tool which can ensure to large extent that at the end you get a successfull build. 


## Hardware Specifications
----------------------------------
<br>
Here is the list of the components that I used for this build. 
<br>


[PCPartPicker part list](https://pcpartpicker.com/list/kTq43F) / [Price breakdown by merchant](https://pcpartpicker.com/list/kTq43F/by_merchant/)

Type|Item|Price
|:----|:----|:----|
**CPU** | [Intel - Core i7-7700K 4.2GHz Quad-Core Processor](https://pcpartpicker.com/product/VKx9TW/intel-core-i7-7700k-42ghz-quad-core-processor-bx80677i77700k) | $328.79 @ SuperBiiz 
**CPU Cooler** | [Corsair - H100i v2 70.7 CFM Liquid CPU Cooler](https://pcpartpicker.com/product/CrDzK8/corsair-cpu-cooler-cw9060025ww) | $91.99 @ Newegg 
**Thermal Compound** | [Arctic Silver - 5 High-Density Polysynthetic Silver 3.5g Thermal Paste](https://pcpartpicker.com/product/6RrG3C/arctic-silver-thermal-paste-as535g) | $11.89 @ OutletPC 
**Motherboard** | [Gigabyte - GA-Z270X-Gaming K7 ATX LGA1151 Motherboard](https://pcpartpicker.com/product/rdtWGX/gigabyte-ga-z270x-gaming-k7-atx-lga1151-motherboard-ga-z270x-gaming-k7) | $183.98 @ Newegg 
**Memory** | [Corsair - Vengeance LED 64GB (4 x 16GB) DDR4-3000 Memory](https://pcpartpicker.com/product/Qz648d/corsair-vengeance-led-64gb-4-x-16gb-ddr4-3000-memory-cmu64gx4m4c3000c15r) | $459.99 @ Newegg Marketplace 
**Storage** | [Samsung - 850 EVO-Series 500GB 2.5" Solid State Drive](https://pcpartpicker.com/product/FrH48d/samsung-internal-hard-drive-mz75e500bam) | $159.99 @ B&H 
**Storage** | [Seagate - Barracuda 2TB 3.5" 7200RPM Internal Hard Drive](https://pcpartpicker.com/product/KyCwrH/seagate-internal-hard-drive-st2000dm001) | $69.89 @ OutletPC 
**Video Card** | [Asus - GeForce GTX 1080 Ti 11GB Founders Edition Video Card](https://pcpartpicker.com/product/dXqbt6/asus-geforce-gtx-1080-ti-11gb-founders-edition-video-card-gtx1080ti-fe) (2-Way SLI) | $687.99 @ SuperBiiz 
**Video Card** | [Asus - GeForce GTX 1080 Ti 11GB Founders Edition Video Card](https://pcpartpicker.com/product/dXqbt6/asus-geforce-gtx-1080-ti-11gb-founders-edition-video-card-gtx1080ti-fe) (2-Way SLI) | $687.99 @ SuperBiiz 
**Case** | [Corsair - Air 740 ATX Full Tower Case](https://pcpartpicker.com/product/2rGj4D/corsair-air-740-atx-full-tower-case-cc-9011096-ww) | $114.99 @ Newegg 
**Power Supply** | [SeaSonic - PRIME Titanium 850W 80+ Titanium Certified Fully-Modular ATX Power Supply](https://pcpartpicker.com/product/74M323/seasonic-prime-850w-80-titanium-certified-fully-modular-atx-power-supply-ssr-850td) | $196.99 @ SuperBiiz 
**Wireless Network Adapter** | [TP-Link - TL-WDN4800 PCI-Express x1 802.11a/b/g/n Wi-Fi Adapter](https://pcpartpicker.com/product/G4H323/tp-link-wireless-network-card-tlwdn4800) | $36.88 @ OutletPC 
**Other** | [Plugable USB Bluetooth 4.0 Low Energy Micro Adapter (Windows 10, 8.1, 8, 7, Raspberry Pi, Linux Compatible; Classic Bluetooth, and Stereo Headset Compatible)](https://pcpartpicker.com/product/2HGj4D/plugable-usb-bluetooth-40-low-energy-micro-adapter-windows-10-81-8-7-raspberry-pi-linux-compatible-classic-bluetooth-and-stereo-headset-compatible) | $21.98 @ PCM 
**Other** | [Rosewill 45 Piece Premium Computer Tool Kit RTK-045](https://pcpartpicker.com/product/j898TW/rosewill-45-piece-premium-computer-tool-kit-rtk-045) | $22.99 @ Amazon 
**Other** | [10 Pairs White Nonslip Dispensing Cleanness Dustless Anti Static Glove](https://pcpartpicker.com/product/tCRFf7/10-pairs-white-nonslip-dispensing-cleanness-dustless-anti-static-glove) | $8.75 @ Amazon 
 | *Prices include shipping, rebates, and discounts* |
 | **Total** | **$3135.08**
 | Generated by [PCPartPicker](http://pcpartpicker.com) 2017-05-16 21:34 EDT-0400 |

