# Home Radiator Smartification

**Rachied Obispo** Mechanical Engineer, Graduated with merit from HAN University of Applied Sciences · [linkedin.com/in/rachied-obispo](https://linkedin.com/in/rachied-obispo)

Motor-driven retrofit that turns a manual radiator valve into a scheduled, phone-controllable heating system with no screws, glue, or other permanent fixings.

![Finished build: the assembly off the radiator (left) and mounted and running (right)](finished-build.jpg)

## Why

Student housing in the Netherlands runs on manual thermostatic radiator valves (TRVs): a dial you turn by hand, no schedule, no remote control. Having grown up in a tropical climate, I wanted to w[...]

Rather than replace the valve with a commercial smart radiator head, I built a small motorized adapter that clamps onto the existing Danfoss valve and turns the stock dial for me, on a schedule, c[...]

## Design constraints

Three constraints shaped the mechanical design more than anything electrical:

- **No permanent fixings -** I was renting, so nothing could be screwed or glued to the wall, the pipe, or the valve body. The entire housing had to clip on and come off clean, which is why it cla[...]
- **Heat -** The housing clamps directly onto the radiator pipe, and standard PLA softens well below what a hot-water pipe can reach. I printed it in PETG instead, its higher heat resistance (glas[...]
- **Compact and out of the way -** This sits on a radiator, a big or ugly housing would have been a daily annoyance. The design had to stay tight to the pipe and out of the way.

## How it works

A 3D-printed housing clips over the radiator pipe and holds a gear-reduced DC motor in line with the valve's thermostatic dial. A gear keyed to the motor shaft meshes directly with a printed gear [...]

**Mechanical:**
- 12 V, 0.7 N·m, 10 RPM DC gearmotor
- Custom 3D-printed gear pair, 41:12 tooth ratio → 3.42:1 torque multiplication at the valve
- 56 mm printed gear ring clamped around the Danfoss dial
- The printed housing that clips onto the radiator pipe

**Electronics:**
- Raspberry Pi 5 as the controller
- Cytron MD10C 10 A PWM motor driver (PWM + DIR + GND from the Pi's GPIO)
- AS5600 magnetic rotary encoder on the motor shaft for closed-loop shaft-angle feedback over I2C
- 12 V→5.1 V buck converter to run the Pi from the same supply as the motor, sized for the combined draw of both
- Single 12 V DC supply for the whole assembly, common ground across supply, buck converter, Pi, driver, and encoder


![CAD assembly](cad-hero.png)

**Full Assembly: With Housing and Rotation Support**



![Labeled component stack](cad-stack-v2.png)


**Labeled Components: Knob gear, Drivetrain gear ratio, DC motor, buck converter, motor controller, Pi 5, AS5600 agnetic rotary encoder**




**Full wiring diagram:**

![Wiring diagram: Raspberry Pi 5 + AS5600 + Cytron MD10C + DC motor](wiring-diagram.png)

**Control:** The Pi runs a scheduler that drives the motor to timed dial positions (e.g., open before I wake up, close before bed) and exposes control to [Home Assistant](https://www.home-assistan[...]

## The moment problem

The Danfoss valve on this particular radiator was old and stiff, turning it took noticeably more torque than a fresh valve would. That exposed a problem the no-permanent-fixings constraint had qui[...]

`Troubleshooting.mp4` is me diagnosing it by hand, isolating whether the motor itself was underpowered or whether the mount was the real problem. It was the mount: the clamp gave the housing one r[...]

The fix couldn't be a screw or a bracket into the wall, that would have broken the original design requirement. Instead I added a series of support wedges along the length of the housing, each sha[...]

## Outcome

The finished system ran the actual heating schedule in my room for about three months, automated, controlled from my phone via Home Assistant when needed, no manual dial-turning. It delivered exac[...]

This was my mechanical engineering degree's "flexible project": a self-chosen, self-scoped assignment worth 80 hours. What the course actually graded wasn't build polish, it was planning, project [...]

## What's in this repo

Because the assignment was graded on planning, management, and presentation rather than on production-grade deliverables, the CAD files and control code were treated as working files, not somethin[...]

- `cad-hero.png` — CAD assembly render
- `cad-stack-v2.png` — labeled CAD component stack (knob, gear ratio, motor, buck converter, motor controller, Pi 5)
- `wiring-diagram.png` — full electrical wiring diagram
- `finished-build.jpg` — the finished unit, off the radiator and mounted/running, side by side
- `Moment Problem.mp4` — the housing spinning around the pipe instead of the knob turning
- `Troubleshooting.mp4` — diagnosing it
- `Moment Problem_Partially Solved.mp4` — the anti-rotation fix, working

## Skills this project drew on

CAD modeling and mechanical design (SolidWorks) · gear/torque calculations · reaction-force and moment analysis · material selection (PETG for heat resistance) · design-for-constraint (no perm[...]
