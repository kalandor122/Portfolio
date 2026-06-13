---
title: "DIY 24W × 8 + 65W USB-C Charging Station from an Old PC PSU"
description: >-
  Build a multi-port USB-C charging station from an old PC PSU and a 3D
  printed case — 8x USB-A QC 3.0 ports, 1x 65W USB-C PD, and a lab bench
  power supply for under $40.
date: 2026-06-10
author: "Füvesi Magor"
tags: [diy, 3d-printing, electronics, charging-station, usb, usb-c, pd, psu]
---

I have a problem: over the past year, I rapidly accumulated devices. Tablet, smartwatch, AirPods, multiple phones, power banks, a laptop. Every single one came with either a slow charger or none at all. Stacking five tiny wall warts on a power strip works until it doesn't. And good GaN chargers? They cost a fortune.

So I built my own charging station. Total cost: **~15,000 Ft** (~$40). It has:

- **8x USB-A ports**, each capable of 24W fast charging (QC 3.0)
- **1x USB-C PD port**, capable of 65W, enough for a laptop
- **A lab bench power supply** (the SK120X module) for when I need adjustable voltage on the bench
- All powered by a salvaged **(bought) 420W PC power supply**
- Housed in a custom **3D printed case** designed in Fusion 360 and printed in PETG

![Finished charging station](/assets/img/posts/charging-station-finished.jpg)
*The completed charging station on the desk — eight USB-A ports, one USB-C PD, and a bench supply in one compact unit.*

![Wiring diagram](https://excalidraw.com/#json=qCJmNCoMCmXQfhtpjYQm5,NjyJEHTbe7gXoDDTya_iTw)
*(Click to open interactive wiring diagram in Excalidraw)*

## The guts

The heart of this build is a 420W ATX power supply I picked up on Vinted for a mere **2,200 Ft**. It puts out plenty of 12V current, and I simply ran six 12V wires from the PSU bundle straight to the modules. No custom PCB, no buck converters, no fuss.

The modules themselves all came from AliExpress:

- **2× 4-in-1 USB QC 3.0 fast charger boards** — eight ports total, each capable of 24W. These are the workhorses for daily device charging.
- **1× IP2368 module** — handles the 65W USB-C Power Delivery for my laptop. Negotiates PD properly so I can charge with a single USB-C cable.
- **1× SK120X adjustable bench power supply** — gives me a variable output for breadboarding, testing, or any random project where a fixed voltage isn't enough.

![Internal modules and wiring](/assets/img/posts/charging-station-internals.jpg)
*The guts exposed — QC 3.0 boards, IP2368 PD module, and the SK120X bench supply wired to the ATX PSU.*

## The case

I knew this needed a proper home. I started with a **Printables model** for the SK120X case, imported it into **Fusion 360**, and modelled the rest of the enclosure around **GrabCAD** files of the other modules. Every cutout, every screw hole, every port position matches the real hardware.

The whole thing was printed on my **upgraded Ender 6** in **PETG**, tough enough to handle the warmth from eight concurrent fast charges without warping. The hand-drawn texture of 3D printing fits the vibe.

![3D printed case close-up](/assets/img/posts/charging-station-case.jpg)
*The custom 3D printed enclosure — every port cutout and screw hole designed in Fusion 360 to match the real modules.*

## Wiring: boring is good

There's no secret sauce in the wiring. The PSU has six 12V wires coming out of its harness. I snipped, stripped, and crimped them onto the input terminals of the USB modules, the IP2368, and the SK120X. Grounds go to ground. That's it. No switch, no fuse, no displays — just raw, reliable power distribution. Sometimes the simplest solution *is* the right one.

## Why not just buy one?

A quality GaN charger with 4 ports runs 10–15,000 Ft these days. A 65W GaN with a single USB-C? Same ballpark. I wanted:

- 8 fast-charge USB-A ports
- A dedicated 65W USB-C PD for my laptop
- A bench supply on top
- Something that looks like it belongs on a desk, not a tangle of wall warts

At 15,000 Ft total, I got all of that, plus the satisfaction of building it myself.

---

*Got questions about the build? Ping me if you want the Fusion 360 files, the STLs, or have wiring questions.*
