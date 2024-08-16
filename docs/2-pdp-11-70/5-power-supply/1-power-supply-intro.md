---
layout: default
title: Power Supply
parent: PDP-11/70
has_children: true
nav_order: 5
---

![](../../assets/images/pdp-11-70/2021-03-17_09.56_Cabinet_header-1-768x75.jpg)

# Power Supply

The power supply of the 11/70 is quite a beast, and we expect to spend some time to ensure it is working properly.

The entire power system is described in detail in chapter 4 of PDP-11/70 maintenance and installation manual (EK-11070-MM)

![](../../assets/images/pdp-11-70/EK-11070-MM-002_Fig_4.1_2.png)

Power System, Physical Location in CPU Cabinet
The power to the CPU goes through three stages in the processor cabinet. First through the 861-E power controller, then through the two H7420 power supplies, each containing four H744 +5V power regulators, before finally connecting through a cable harness to the CPU backplane and the front panel.

![](../../assets/images/pdp-11-70/EK-11070-MM-002_Fig_4.3-1024x773.png)

Processor Cabinet Power Connections
In addition, there are two 5411086 modules, one in each H7420. One provides +8V and +15V as well as a line clock. The other one provides -15V.

![](../../assets/images/pdp-11-70/EK-11070-MM-002_Fig_4.2-1024x488.png)

Typical PDP-11/70 Power System

The physical locations for each regulator can be found in the table below.

![](../../assets/images/pdp-11-70/EK-11070-MM-002_Table_4.1-768x962.png)

## 861-E Power Controller

The power control unit is controlling and distributing power to all parts of the system, possibly through other power control boxes in other racks. It is a fairly simple device, as seen from the schematic below.

The 861-E is intended for 180-264V (312-458V phase to phase), while the 861-D version is for 90-132V (156-229V phase to phase).

![](../../assets/images/pdp-11-70/EK-11070-MM-002_Fig_4.13-1024x890.png)

861-E Simplified circuit schematic

![](../../assets/images/pdp-11-70/2021-03-06_17.42_Power_controller-1024x327.jpeg)

This is what it looks like on the bench after an initial cleaning of the exterior.

![](../../assets/images/pdp-11-70/2021-03-07_08.08_Power_controller_2-1024x760.jpg)

Looks good on the inside as well.

![](../../assets/images/pdp-11-70/2021-03-07_08.10_Power_controller-1024x726.jpeg)

The capacitor on the pilot control board checked out fine (54uF, ESR=0.7ohm)

The capacitance was measured from each phase (and neutral) to ground in the power connector to check the capacitors in the line filter. In these measurements, some capacitance was probably added from the long power cable. The capacitors across the switched outputs were also measured (C1 and C2 in the schematic above). Specified and measured values are listed in the table below.

  Capacitor location    specified  Measured   Vloss
  Line filter, phase 1  30nF       51nF       0.3%
  Line filter, phase 2  30nF       47nF       0.3%
  Line filter, phase 3  30nF       47nF       0.3%
  Line filter, neutral  30nF       47nF       0.3%
  Output, phase 1       100nF      106nF      0.1%
  Output, phase 2       100nF      107nF      0.1%
  Output, phase 3       100nF      100nF      0.1%

When taking the power controller out of the CPU cabinet, the 3 phase plug had to be removed. It looked like it had been running quite hot, and the isolation on the cables near the plug was brittle. 10-15 cm of the cable was cut off before the plug was mounted.

![](../../assets/images/pdp-11-70/2021-03-06_16.04_3phase_plug_1-e1615874322532-768x1025.jpeg)
![](../../assets/images/pdp-11-70/2021-03-07_07.50_3phase_plug-e1615874356744-712x1024.jpeg)

3 phase power plug before and after

![](../../assets/images/pdp-11-70/2021-03-07_07.56_3phase_plug-1024x768.jpeg)

Only serious computers have 400V 3 phase plugs

Everything now looks fine in the power controller, but we are not able to fully test it until we have access to a 230V three phase outlet, i.e. 400V between phases (not commonly available in Norwegian domestic buildings).

![](../../assets/images/pdp-11-70/EK-11070-MM-002_Fig_3.8.png)

Power plugs used on the 861-E and corresponding cables to power supplies.

At least as a temporary solution, we should build converter cables from the NEMA 6-15R 250V plugs (see above) to the European style plug to connect the power supplies directly to mains instead of through the 861-E.

A couple of these should work: https://no.mouser.com/ProductDetail/Qualtek/Q-722-BW?qs=BXmE%252BJ0Y7xam28jusjp7Eg==

## 7420 Power Supply

This is the big and heavy part! It contains a massive transformer, up to five regulators and four 240V fans. Each +5V regulator will be removed and tested separately.

![](../../assets/images/pdp-11-70/XL6qTRW.png)

In the main body we find the transformer and the 5411086 regulator and monitor board. They are described on page 4-51 in EK11-11070-MM.

## H744 Regulator

The H744 regulator is the component that in our experience fails most frequently. Each regulator must be tested on the bench.

![](../../assets/images/pdp-11-70/2021-03-23_19.57_Regulator-1024x905.jpeg)

First H744 regulator on the bench

Page 4-59 in EK-11070-MM describes the H744 regulators and on page 4-87 there are suggestions on how to diagnose a faulty regulator.

Schematics can be found here:
http://www.bitsavers.org/pdf/dec/pdp11/1170/EY-D3054-HO-002_45-70hw.pdf
http://dustyoldcomputers.com/pdp-common/reference/drawings/modules/h/h744.pdf

Each H744 regulator was tested separately in a setup similar to Figure 4-56 in the EK-1070-MM document (see below). The variac was adjusted slowly to increase the AC input voltage to the regulator to approximately 25V. A Python program was developed to control the electronic load (HP 6060B) and DMM (Fluke 45) over GPIB to gradually increase the output current from 0 to 20 A and measure the voltage.

![](../../assets/images/pdp-11-70/EK-11070-MM-002_Fig_4.56-1024x418.jpg)
![](../../assets/images/pdp-11-70/2021-05-16-H744-Test-setup-712x1024.jpeg)
Test setup

To our surprise, all 7 regulators worked flawlessly. The output voltage was adjusted to 5.1V at 10A, but this may need to be adjusted again once the regulators are re-inserted into the cabinet and any voltage drop in the wire harness can be accounted for.

![](../../assets/images/pdp-11-70/2021-05-25-H744-Load-test-1024x686.png)
Output voltage at different loads for all 7 regulators

The regulated output waveform was similar to the one depicted in the maintenance manual. Some spikes should be expected according to the experts.

![](../../assets/images/pdp-11-70/EK-11070-MM-002_Fig_4.39.jpeg)
![](../../assets/images/pdp-11-70/2021-05-16-H744-Output-waveform-1024x768.jpeg)

Regulator output waveforms

The only components that needed to be replaced were the light bulbs, which were obviously burnt out after many years of service. Instead of replacing with LEDs, 5 V light bulbs were used to give the authentic glow.

![](../../assets/images/pdp-11-70/2021-05-23-Light-bulbs-1024x578.jpeg)

Old light bulbs were replaced with new ones

All H744 regulators are now tested and ready to be re-installed in the power supplies.

![](../../assets/images/pdp-11-70/2021-05-22-H744-1024x372.jpeg)

All seven fully functional 5V regulators on the bench

## Wire harness

The whole power system is tied together with a rather impressive wire loom which connects to the CPU backplane. We will inspect it for damage as the cables might have dried out or got pinched.

![](../../assets/images/pdp-11-70/oslvhid.png)

## Backplane

The last endevour in making sure the power supply is working properly means taking out all of the cards in the card cage and inspect for debris and damage. At this stage we can connect the power supply to the backplane and turn the power on. EK-11070-MM lists test points on the backplane were we will double check voltages before beginning to populate the system with cards and move on to testing the CPU.

The expected voltages at the backplane can be found in the table below.

![](../../assets/images/pdp-11-70/EK-11070-MM-002_Table_3.1-1024x726.png)

The card chassi contains ten(10!) 240V fans that we should take the oportunity to test and maybe service.
