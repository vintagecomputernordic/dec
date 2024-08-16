---
layout: default
title: Power Supply
parent: PDP-11/70
has_children: true
nav_order: 5
---

![](../../../assets/images/pdp-11-70/2021-03-17_09.56_Cabinet_header-1-768x75.jpg)

# Power Supply

The power supply of the 11/70 is quite a beast, and we expect to spend some time to ensure it is working properly.

The entire power system is described in detail in chapter 4 of PDP-11/70 maintenance and installation manual (EK-11070-MM)

![](../../../assets/images/pdp-11-70/EK-11070-MM-002_Fig_4.1_2.png)

_Power System, Physical Location in CPU Cabinet_

The power to the CPU goes through three stages in the processor cabinet. First through the 861-E power controller, then through the two H7420 power supplies, each containing four H744 +5V power regulators, before finally connecting through a cable harness to the CPU backplane and the front panel.

![](../../../assets/images/pdp-11-70/EK-11070-MM-002_Fig_4.3-1024x773.png)

_Processor Cabinet Power Connections_

In addition, there are two 5411086 modules, one in each H7420. One provides +8V and +15V as well as a line clock. The other one provides -15V.

![](../../../assets/images/pdp-11-70/EK-11070-MM-002_Fig_4.2-1024x488.png)

_Typical PDP-11/70 Power System_

The physical locations for each regulator can be found in the table below.

![](../../../assets/images/pdp-11-70/EK-11070-MM-002_Table_4.1-768x962.png)
