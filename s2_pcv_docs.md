# s2-pcv-docs

Ok, nintendo seems to have rewrote all of pcv. so here's what we know.
And this will affect any OC tool

# TLDR
Horizon OC for Switch 2 (Sky OC) will be coming but not for a while.
And it will not be as advanced as S1 OC.
But it will be more advanced than sys-clk or the other primative S1 OC tools

## clock tables
clock tables don't seem to exist here, they seem to be generated at runtime.
i cant verify this fully yet (still have to get Ghidra cooperating with ARMv8.2 PAC), but if this is true then the 561/1007mhz figure for gpu and 998/1122mhz figure for cpu that leaked aren't true.

## power management
pcv does not do power management on S2.
It offloads it to another service- "bpmpmr"
https://switchbrew.org/wiki/Switch_2:_BPMP_services

## DRAM
dram is likely trained in pcv, but I won't touch it at all as modifying dram timings/all without nand backup is horrible idea
eitherway it uses LPDDR5X chip and thats rated from 3200MHz (Samsung), 3750MHz (Micron) and 4267MHz (SKHynix)
and since lpddr5x training/fsp is hell, dont expect anything here.
102gb/s is enough, and S2 DRAM run at 3200mhz (max that all consoles can do, so "OC" will be very situational)

## cpu
CPU only OC. NO CPU UV .
WHY- even though its theoretically possible on S2 I don't have any NAND backup so I cant restore anything.
and bad CL-DVFS tuning on S1 causes even faster nand corruption than bad DRAM OC (B3711 had nand corruption 30+ times trying to find optimal tuning on S1)

## gpu
this is the once to be exited about.
since GPU (GA10F) is software controlled, it can be OC/UV as much as we want.
So expect GPU to 1.4GHz from 1007MHz (if the rating leak is correct)

## voltages
I measured S2 CPU/GPU voltage ages ago, before it was even documented on switchbrew.
It uses 2 DA9092 PMIC connected to same I2c bus.
CPU Voltage 510mV
GPU Voltage 550mV
now this doesnt match up with whats on SB, so I think S2 uses per unit binning, like S1 GPU.
And maybe even for CPU, although N only did per unit binning on S1 for CPU on erista, not on mariko

## die shrink
RANT time:
i hate that ns2jb released now, i wish they held on to it.
would have loved to OC/UV die shrink and to poke at the die shrink hw.
sure you get exploit on 23.0.1, but its going to be stuck there
so lets pray for kernel fuckup in post FW 23 or HW errata causing security issue.
END OF RANT