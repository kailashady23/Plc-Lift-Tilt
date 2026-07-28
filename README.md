**Automated Lift and Tilt Control System (PLC)**

A PLC-controlled pneumatic lift and tilt platform with full safety interlocking, built to respond to floor requests, hold position accurately, and prevent unsafe mechanical states.

**Problem**

Design, implement, and troubleshoot a system that lifts a platform between three floor levels and tilts it left/right, using pneumatic actuators under PLC control — with safety interlocks so conflicting commands (e.g., tilting both directions at once) can never occur.

**System Architecture**

_Three integrated subsystems:_

1. Electrical — buttons, floor/tilt limit switches, E-stop, indicator lamps (inputs/outputs wired to the PLC)

2. PLC Controller (Allen-Bradley, programmed in Studio 5000 Logix Designer, ladder logic) — processes inputs and issues motion commands

3. Pneumatic — double-acting lift cylinder (5/3-way valve) and left/right tilt cylinders, with flow control valves for smooth motion and a fail-safe retract circuit if the PLC loses power

**Control Logic (Ladder Logic)**

1. Floor selection: push-buttons set a TargetLevel tag (0/1/2); limit switches continuously report CurrentLevel

2. Lift motion: LiftUpCmd/LiftDwnCmd are driven by a live comparison of TargetLevel vs CurrentLevel — the lift moves automatically until it reaches the requested floor, then de-energizes precisely (no override drift)

3. Tilt safety interlock: left and right tilt solenoids are mutually exclusive by design — the left solenoid can only energize if the right tilt limit sensor is not active, and vice versa, preventing mechanical conflict

4. Fail-safe design: a normally-closed E-stop valve cuts air supply immediately on activation; a spring-return valve forces the cylinder to retract automatically if the PLC crashes or loses power

5. Operator feedback: indicator lamps show current floor, tilt direction, system-enable state, and E-stop/fault status in real time

**Why This Matters**

This project is a compact example of designing for fail-safe behavior first — the interlocks and fail-safe retract logic mean the system defaults to a safe state under fault conditions rather than an undefined or dangerous one, which is a core principle in industrial and safety-critical automation.

**Team**

Built with a teammate (Gurjot Singh) for the Pneumatics/Hydraulics/Automation course at Algonquin College.

**Files in this repo**

- /ladder-logic — full PLC rung documentation (floor requests, lift movement, tilt logic, indicators)
  ladder-logic.md

- /diagrams — pneumatic circuit diagrams and I/O wiring layout
