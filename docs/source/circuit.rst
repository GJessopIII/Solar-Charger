Schematic and PCB Design
========================

In general the circuit design is very simple, the block diagram below shows each subsystem that makes up the entire circuit.

.. figure:: Pictures/BlockDiag.png
   :width: 400px
   :align: center
   :height: 125px
   :alt: Block Diagram
   :figclass: align center

   Overall circuit Block Diagram

In this circuit there is a MPPT charge controller that charges the attached 1S Lipo Battery(3.2V @ 0% to 4.2V @ 100%) which is then boosted to 5V to charge anything attached to the USB output.  

MPPT Charging Circuit
---------------------

Many IC's exist out there that are able to do MPPT tracking for small solar cells like the 2.5W panel we are using. In order to simplify the design of the circuit I chose an existing IC that would do MPPT for me. Researching existing IC's I found that the best IC for what I need is the LTC3652. The LTC3652 is a readily avaliable IC on digikey and is made by Linear Technologies. There do exist chinese clones of this chip however they were not as readily avaliable and so my design was based around the LTC3652 instead. :download:`Datasheet <Datasheets/LT3652.pdf>`

Design of the components that supported the LT3652 was accomplished through close investigation of the datasheet and what was recommended by Linear Technologies. Once values were found for these components it was simulated in order to see if it had the desired response. 

Boost Converter
---------------

Once we have the battery charging we now need a boost converter in order to output the desired 5V from the 3.6V battery voltage. This was an easy decision thanks to digikey's organized database of boost converters. Specifications that the boost converter must fulfill are an input that can handle 3.6V and an output of 5V that can handle up to 2A. Eventually, I found the RT4812 made by Richtek which has all of the necessary specifications. Just as before I also considered chinese alternatives however found the shipping took too long for the timeframe that was required. :download:`Datasheet <Datasheets/RT4812.pdf>`
Unfortunately this IC was not made by Linear Technologies which meant that there is not an existing simulation of this circuit causing design to be a little more arduous. Luckily, this IC had much supporting components and many of then are common across all IC application circuits such as bypass capacitors meaning that these values were very easy to obtain since they are in the datasheet. The RT4812 did also require a large inductor and capacitor as do all boost converters, which again has recommended values in the datasheet making design much easier. One thing that was necessary to design was to find the values for the resistors in the feedback network that give the desired 5V output. Using the provided equations

.. math::

   R_1 = R_2(\frac{V_{out}}{V_{FB}}-1)

where :math:`V_{FB} = 500mV` and :math:`V_{out} = 5V`. Choosing :math:`R_2 = 200k \Omega` we can easily find that :math:`R_1 = 1.8 M\Omega`. Which is the last portion of design for this IC.  

Lipo Charge Protection
----------------------

Built into the LT3652 is overcharge protection. However, the boost converter that converts the 3.6 V to 5V does not have overdischarge protection. It is very unhealthy for a lipo battery to discharge below 3.0 V as it will cause permanent damage that may not be recovered from. This was accomplished by use of a seperate IC the S-8261, which required two N channel MOSFETS which was accomplished by a dual package DMG6968UDM. When the lipo battery would get down to a dangerous level of around 3.0V the MOSFETs would disengage and disconnect the battery from the shared ground causing the battery to longer be connected to the boost converter.   

Results
=======
Running tests on the solar charger circuit, once everything was working, I started by first measuring the efficiency of the boost converter to verify its operation. Results are tabulated below

+------------+-------------+----------+
|Measurement |        Input|     Ouput|
+============+=============+==========+
|Current     |      0.587 A|    0.43 A|
+------------+-------------+----------+
|Voltage     |      4.064 V|    4.99 V|
+------------+-------------+----------+
|Power       |      2.385 W|    2.15 W|
+------------+-------------+----------+

which yields an efficiency of :math:`\eta = \frac{P_{out}}{P_{in}} = \frac{2.15}{2.385} = \boxed{89\%}`. This verifies that the boost converter is indeed operating at acceptable efficiency. 

Next was to find the efficiency of the solar charger as well as the amount of power it draws from the solar panel. 

+------------+----------------------+-----------------+
|Measurement |Input(direct sunlight)|Ouput(to battery)|
+============+======================+=================+
|Current     |               0.103 A           0.171 A|
+------------+----------------------+-----------------+
|Voltage     |                  10 V|           4.20 V|
+------------+----------------------+-----------------+
|Power       |                1.03 W|          0.714 W|
+------------+----------------------+-----------------+

which yields an efficiency of :math:`\eta = \frac{P_{out}}{P_{in}} = \frac{0.714}{1.03} = \boxed{69\%}`. This efficiency does seem a little low and does have some concerns. However, I believe this can be fixed by increasing the size of the traces as well as double checking to make sure that no components are causing unnecessary power loss by being too small or otherwise.  


Design Files
============

I would recommend cloning the `repository <https://github.com/cosgais/Solar-Charger>`_ and then installing `KICAD <http://www.kicad-pcb.org/>`_ and `LTSpice <https://www.analog.com/en/design-center/design-tools-and-calculators/ltspice-simulator.html>`_ in order to properly view all of the design files. 

Schematic and PCB
-----------------
In order to avoid the risk of a picture being outdated I am just going to have a link to the repository where the schematic and PCB files are located `here <https://github.com/cosgais/Solar-Charger/tree/master/ChargePCB>`_. However, I would recommend cloning the repository and opening the .pro in KICAD. 
If KICAD is not already installed it is very simple to install and can be downloaded `here <http://www.kicad-pcb.org/>`_.

BOM
---
Bill of materials from this project is located on the repository and was generated by digikey. Meaning if you have a digikey account you should be able to import the excel file into your account and all the correct parts will be added. Excel file is located `Here <https://github.com/cosgais/Solar-Charger/tree/master/ChargePCB/BOM>`_.

Simulation Files
----------------
Linear Technologies makes a great simulation software called LTSpice which includes all of the IC's that they manufacture. Having these models available makes the design process much simpler. If you want to run the simulation files first install the LTSpice software and then open the .asc files from the repository. 

Simulation files can be found `Here <https://github.com/cosgais/Solar-Charger/tree/master/LTC3652%20Simulation>`_. 
