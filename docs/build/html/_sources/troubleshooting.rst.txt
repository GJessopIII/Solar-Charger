Troubleshooting
================

Problem 1 (Fixed)
-----------------
Initially I found out that the biggest problem I faced was because I had missed one zone priority allocation. This caused the ground plane to bleed into the zones that I had used for large tracks that connected to the IC's. (Insert Picture)

This was remedied by using a razor blade in order to cut the traces to disconnect the ground plane where it shouldn't have been connected. (Insert Picture)

Then a simple change to the zone allocation in the PCB files were applied which fixes the problem in all future revisions. 

Problem 2 (In Progress)
-----------------------
When taking the charger out into the sun and turning on the boost converter there seems to be a solid 5V on the USB output. However, if I add any load to the output the circuit is unable to charge anything. Also, putting an ammeter in series with the battery and the solar charging circuit shows that there is very little current that is flowing. These things lead me to believe that the battery is somehow no connected to the circuit where it is supposed to be. This could be caused by just a misconnection of the circuit or maybe the lipo overcharge and overdischarge circuit is working too well. I think a good first test is to completely bypass the protection circuitry for now by connecting the negative terminal of the batter directly to ground instead of running it through the protection circuitry. 
