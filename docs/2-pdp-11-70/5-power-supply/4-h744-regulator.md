---
layout: default
title: H744 Regulator
parent: Power Supply
grand_parent: PDP-11/70
nav_order: 4
---

![](/assets/images/pdp-11-70/2021-03-17_09.56_Cabinet_header-1-768x75.jpg)

# H744 Regulator

The H744 regulator is the component that in our experience fails most frequently. Each regulator must be tested on the bench.

![](/assets/images/pdp-11-70/2021-03-23_19.57_Regulator-1024x905.jpeg)

First H744 regulator on the bench

Page 4-59 in EK-11070-MM describes the H744 regulators and on page 4-87 there are suggestions on how to diagnose a faulty regulator.

Schematics can be found here:
http://www.bitsavers.org/pdf/dec/pdp11/1170/EY-D3054-HO-002_45-70hw.pdf
http://dustyoldcomputers.com/pdp-common/reference/drawings/modules/h/h744.pdf

Each H744 regulator was tested separately in a setup similar to Figure 4-56 in the EK-1070-MM document (see below). The variac was adjusted slowly to increase the AC input voltage to the regulator to approximately 25V. A Python program was developed to control the electronic load (HP 6060B) and DMM (Fluke 45) over GPIB to gradually increase the output current from 0 to 20 A and measure the voltage.

![](/assets/images/pdp-11-70/EK-11070-MM-002_Fig_4.56-1024x418.jpg)
![](/assets/images/pdp-11-70/2021-05-16-H744-Test-setup-712x1024.jpeg)
Test setup

To our surprise, all 7 regulators worked flawlessly. The output voltage was adjusted to 5.1V at 10A, but this may need to be adjusted again once the regulators are re-inserted into the cabinet and any voltage drop in the wire harness can be accounted for.

![](/assets/images/pdp-11-70/2021-05-25-H744-Load-test-1024x686.png)
Output voltage at different loads for all 7 regulators

The regulated output waveform was similar to the one depicted in the maintenance manual. Some spikes should be expected according to the experts.

![](/assets/images/pdp-11-70/EK-11070-MM-002_Fig_4.39.jpeg)
![](/assets/images/pdp-11-70/2021-05-16-H744-Output-waveform-1024x768.jpeg)

Regulator output waveforms

The only components that needed to be replaced were the light bulbs, which were obviously burnt out after many years of service. Instead of replacing with LEDs, 5 V light bulbs were used to give the authentic glow.

![](/assets/images/pdp-11-70/2021-05-23-Light-bulbs-1024x578.jpeg)

Old light bulbs were replaced with new ones

All H744 regulators are now tested and ready to be re-installed in the power supplies.

![](/assets/images/pdp-11-70/2021-05-22-H744-1024x372.jpeg)

All seven fully functional 5V regulators on the bench
