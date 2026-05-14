\# plc-codesys-motor-control



A PLC program that controls a motor with start/stop, fault detection, and auto-restart logic.



\---



\## What This Demonstrates



\- Ladder Logic programming in CoDeSys

\- Motor control logic (start/stop, seal-in circuits)

\- Fault detection and fault handling

\- Auto-restart timer logic

\- Motor feedback signals

\- Retry counter with permanent fault escalation

\- Structured Text rewrite (in progress)



\---



\## The Problem



In pump applications, motors can experience transient faults — brief overloads or 

blockages that clear on their own — making automatic restart preferable to requiring 

an operator to manually intervene after every fault event. This program automates 

that cycle: detecting faults, attempting timed restarts, and escalating to a permanent 

fault state after a defined number of retries — protecting the motor from damage caused 

by repeated restarts against an unresolved condition.



\---



\## Implementation Decisions



\*\*Why two revisions?\*\*

Rev 1 was built as a minimal functional program — start/stop, fault detection, and 

auto-restart. After testing, a clear gap emerged: nothing prevented the program from 

restarting indefinitely against an unresolved fault. Rev 2 added a retry counter, 

motor feedback signals, and permanent fault escalation to address that.



\*\*Why Ladder Logic?\*\*

Ladder Logic was chosen as the primary language due to its dominance in industrial 

automation — it's the language most maintenance technicians and controls engineers 

will encounter on the floor. Extending rev 1 into rev 2 within the same language was 

the practical choice; switching to Structured Text mid-project would have added 

complexity without solving the immediate problem. A full ST rewrite is planned as a 

separate exercise to demonstrate language portability.



\*\*How does fault escalation work?\*\*

Fault escalation is based on duration and count. A fault must persist longer than a 

5-second threshold before it increments the retry counter — this filters out transient 

faults that clear quickly. After 3 consecutive threshold-exceeding faults, the program 

sets a permanent fault flag that locks out the motor and requires manual reset. The 

5-second threshold and retry count of 3 were chosen for simulation purposes and would 

be configured to application requirements in a production deployment.



\---



\## Demo



\*Video walkthrough: \[link pending]\*

\*Screenshots: \[pending]\*



\---



\## How to Run



\*\*Requirements\*\*

\- CoDeSys V3.5 SP22 Patch 1 or compatible version



\*\*Steps\*\*

\*\[To be completed after clone and run verification]\*



\---



\## Reflection



\*\*What I would do differently\*\*

In hindsight, the motor feedback timer added complexity that made the demo harder to 

follow cleanly. If starting over, I might scope rev 2 more narrowly. That said, I kept 

it because feedback signals are standard in real motor control applications — removing 

it would have made the program easier to demo but less representative of what you'd 

find on a plant floor.



\*\*What building this taught me\*\*

What surprised me was how quickly a simple motor control program grows in complexity 

once you account for safety — both equipment protection and operator safety. A motor 

that restarts indefinitely against an unresolved fault risks equipment damage and 

creates a safety hazard for anyone nearby. That realization drove the escalation logic 

in rev 2 more than anything else.



\*\*What this unlocks\*\*

This project established a working understanding of the discrete inputs, outputs, and 

signals common in industrial control systems. That foundation directly unlocks the next 

areas of study: industrial networking — how those signals move between devices — and 

Structured Text, which I'll apply in the next revision of this same program to 

demonstrate language portability across the same control problem.



\---



\## Tags



`PLC` `Ladder Logic` `CoDeSys` `Motor Control` `Fault Detection` `Auto-Restart` 

`Industrial Automation` `Controls Engineering` `Structured Text`

