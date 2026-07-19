---
title: "I Turned My Ender 3 Into a Pen Plotter and Wrote My Own Slicer"
description: >-
  Converting an unused Ender 3 into a pen plotter with a from-scratch SVG
  slicer written in pure Python. Zero dependencies, parametric Bezier
  curves, and custom G-code generation.
date: 2026-07-19
author: "Füvesi Magor"
tags: [python, svg, g-code, plotter, ender-3, 3d-printer, diy, maker, bezier]
---

My Ender 3 sat on a shelf for months. I bought it like everyone does, printed a few things, then the bed leveling drifted, the nozzle clogged, the first layer stopped sticking, and I just didn't have the patience to go through the full recalibration cycle. So it collected dust.

Then I saw a TikTok video of someone using their 3D printer as a pen plotter. Clip a pen to the toolhead, feed it SVG paths instead of 3D models, and it draws on paper. The printer follows coordinates regardless of whether it's extruding plastic or dragging a pen. That was enough reason to try.

## The hardware is the easy part

Converting an Ender 3 to a pen plotter takes about ten minutes. Print a pen holder from Thingiverse, screw it onto the X-axis carriage, adjust the Z offset so the pen touches paper when Z is at zero. The printer thinks it's printing. It's actually drawing.

The interesting part is software. You need something that takes a drawing and turns it into coordinates the printer can follow: a slicer.

## Why I wrote my own slicer

There are existing tools. Inkscape has a G-code plugin. There's vpype, svg2gcode, and a dozen others. I could have used any of them.

But I had a specific idea for how the flow should work. Parse an SVG, pull out the path data, convert the Bezier curves to parametric equations, sample points evenly along each curve, emit G-code that traces those points. No magic, just math. It also sounded like a fun challenge. Writing a slicer makes you think about curve math in a way that using one doesn't.

## How the slicer works

The tool is a single Python file, about 250 lines, no dependencies beyond the standard library. Three output modes:

**Desmos equations (default).** Prints copy-paste parametric equations for every curve in the SVG. Useful for visualizing the math before committing to hardware. Paste them into Desmos, set a slider from 0 to 1, watch the curves render.

**CSV.** Samples each curve at `n` evenly spaced parameter values and writes a table of (path, segment, t, x, y). Handy if you want to process the points in another tool.

**G-code.** Generates plotter-ready G-code. Moves the toolhead to the start of each curve, lowers the pen, traces the sampled points, raises the pen, moves to the next curve.

### The pipeline

Tokenize, resolve, flip Y, sample.

**Tokenize.** The SVG `d` attribute string gets split into commands (`M`, `C`, `Q`, `L`, `V`, `H`, `Z`) and numeric coordinates.

**Resolve.** Relative commands become absolute coordinates. `Z` (close path) inserts a line back to the subpath start.

**Flip Y.** SVG uses Y-down coordinates. The slicer inverts Y using the viewBox height so the output is Cartesian (Y-up), which is what the printer expects.

**Sample.** Each curve segment (cubic Bezier, quadratic Bezier, or straight line) gets evaluated at `n` evenly spaced values of the parameter `t` ∈ [0, 1].

For cubic Beziers:

```
P(t) = (1-t)³·P₀ + 3(1-t)²·t·P₁ + 3(1-t)·t²·P₂ + t³·P₃
```

Quadratic and linear segments use simpler versions. The first point of each segment overlaps the last point of the previous one, so the path stays continuous. Between segments, the pen lifts.

### Usage

```bash
# Preview the math
python main.py drawing.svg

# Sample points
python main.py drawing.svg --csv points.csv --n 20

# Generate G-code for the plotter
python main.py drawing.svg --gcode output.gcode --n 20
```

Tune sampling density with `--n` and pen lift/drop heights with `--z-up` and `--z-down`.

## What I learned

Writing an SVG path parser by hand is the kind of thing that sounds tedious and is tedious. But you come out the other side with a real understanding of how vector graphics work. The Bezier math is satisfying: three different curve types, same `P(t)` evaluation pattern, just different polynomial degrees.

The G-code generation was anticlimactic in the best way. The printer doesn't need anything fancy. A sequence of `G00` rapid moves. If the coordinates are right, the pen follows.

## The result

It draws. Feed it an SVG and the printer that was collecting dust traces it onto paper. The `smile.svg` test file produces 32 curve segments, 20 points each, a few hundred lines of G-code.

There are existing tools that do this with more features. But I understand every line of this one, and it works exactly how I want.

Source: [github.com/kalandor122/slicer](https://github.com/kalandor122/slicer). Single Python file, zero dependencies. If you have an old printer gathering dust.

---

*Stack: Python · SVG · Bezier curves · G-code · Ender 3 · Pen Plotter*
