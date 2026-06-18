---
title: "Fixing a Logitech MX Master 3s for 7,000 Ft"
description: >-
  Bought a broken MX Master 3s on Vinted, replaced the faulty left click
  button with a soldering iron and an AliExpress part. Total cost: 7,000 Ft
  instead of 40,000 Ft.
date: 2026-06-18
tags: [diy, electronics, mouse, logitech, soldering, repair]
---

The MX Master 3s regularly shows up on "best mouse" lists, and for good reason: the ergonomic shape, the MagSpeed scroll wheel, the side scroll, the USB-C charging. It retails for around 40,000 Ft in Hungary. That's a lot for a mouse.

So when I spotted one on Vinted for 5,000 Ft (shipping included), I took a closer look. The seller's description said the left mouse button "rarely works." That sounded like a microswitch problem to me, which is one of the easiest things to fix on a mouse.

## The parts

**From Vinted:**
- Logitech MX Master 3s, left click intermittently dead — **5,000 Ft** with shipping

**From AliExpress:**
- Replacement microswitches (I bought a pack of 10, only needed 1) — **~2,000 Ft** with shipping
- New PTFE mouse skates (ended up not needing them, the originals were fine) — included in that 2,000 Ft

**Total: 7,000 Ft** for a mouse that goes for 40,000 Ft new. That's an 82% discount, if you don't count the hour I spent taking it apart.

## The teardown

iFixit has a guide for the MX Master 3s, and it's solid. The short version:

1. Peel off the skates (the ones on the bottom). There are screws underneath.
2. Pop the top shell off. It clips in, but not aggressively.
3. Disconnect the ribbon cable connecting the top shell buttons to the main board.
4. You're in.

The inside is clean. Logitech doesn't go crazy with glue, which I appreciate. The left click microswitch is a tiny Kailh GM 8.0 on a small daughter board, held in by a single screw.

## The soldering

This is the part where a lot of people would say "I don't have the tools for this." You probably do. A cheap soldering iron from AliExpress (the kind that plugs into USB-C and runs off a phone charger) is enough for this job. You also need:

- Solder wick or a solder sucker to remove the old solder
- Fresh solder (lead-free is fine, leaded is easier to work with)
- Tweezers
A steady hand.

I desoldered the three pins holding the old microswitch to the board, pulled it off, dropped the new one in, and soldered it back. The whole soldering job took maybe 10 minutes. The new switch clicks a lot more crisply than the old one, which probably explains why the left button was failing: the internal contact was worn out.

## Putting it back together

Reverse of disassembly. Screw the daughter board back in, reconnect the ribbon cable, clip the top shell on, screw it together, stick the skates back on.

One thing I'll note: the ribbon cable is fiddly. It's a ZIF (zero insertion force) connector, which means there's a tiny latch you flip up to release the cable, then flip down to lock it. If you're not careful, you can break the latch and then the cable won't stay seated. The ifixit guide has a nice warning that i thankfully followed

## Was it worth it?

I got a 40,000 Ft mouse for 7,000 Ft and an hour of my time. The repair itself was straightforward, maybe a 3/10 on the difficulty scale. The hardest part was peeling off the old skates without wrecking them, and I ended up not even needing to remove them fully.

If you're comfortable with a soldering iron (or willing to learn on a cheap project like this), mouse microswitch replacement is one of the most satisfying repairs you can do. The parts cost almost nothing, the risk is low, and you end up with a mouse that works better than new because you picked the switch you wanted.

The MX Master 3s is a great mouse. At 7,000 Ft, it's a no-brainer.

---

*Got questions about the repair or want to know what switch I used? Ping me.*
