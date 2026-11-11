# Mike Holcomb — Getting Started in ICS/OT Cyber Security

## Part 1: Overview

- **HMI (Human-Machine Interface)** is not just a picture of the plant. The operator *controls* the process through it: opens and closes valves, starts and stops pumps, changes setpoints, acknowledges alarms.
- The HMI doesn't drive equipment itself. It sends commands to a controller (PLC or DCS), and the controller runs the logic and moves the field devices. If the HMI dies, the plant keeps running; the operator just loses the view.
- **Attacker on the HMI** — in IT the first worry is stolen data. In OT it's the last one. The real risks, in order:
  1. Sending commands to the process (open a valve, stop a pump) — Ukraine 2015: attackers used operators' own HMIs remotely to open breakers.
  2. Lying to the operator (manipulation of view) — the screen shows "normal" while the process isn't. Stuxnet replayed normal values to operators.
  3. Taking the view away (loss of view) — operator is blind and has to shut down to stay safe.
- Worst case is harm to people and the environment. The last layer that should prevent it is the **SIS** (Safety Instrumented System), independent from the control system. That's why the 2017 TRITON/TRISIS attack going after a Triconex SIS was such a big deal.

### Scenario check (2026-11-10)
HMI shows sump at 20%, I can see it's nearly full, operator's mouse moved by itself.
- First: safety and the process, not the diagnosis. Don't pump blind, tell the operator the real level.
- Field verification with a local gauge beats the screen. A person in the field is the last defense against manipulation of view.
- Most likely cause is a failed or plugged level transmitter. The moving mouse still gets escalated to whoever owns the control system.
- Don't touch the HMI, don't pull cables, don't reboot, don't post photos, don't declare an attack yourself.

### Cert path Mike suggests vs my roadmap
| Mike | My roadmap | Why |
|---|---|---|
| CompTIA Network+ | CCNA 200-301 | Alberta integrators and utilities run Cisco; OT network folks respect CCNA more. |
| CompTIA Security+ | Security+ | Same. HR filter. |
| CompTIA SecOT+ | Check at phase 3 | New cert, market recognition in Canada still unknown. |
| SANS GICSP / GRID / GCIP | Later, employer-paid | ~USD 9k+ each with the course. GCIP matters for NERC CIP (BC Hydro). |
| ISA/IEC 62443 series (4) | Fundamentals Specialist at phase 3, Risk Assessment optional | Job postings ask for 62443 by name. |