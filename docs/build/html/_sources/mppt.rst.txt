Maximum Power Point Tracking (MPPT)
===================================

Maximum Power Point Tracking (MPPT) uses the well know fact that in order to extract the maximum power from a source you must match the impedance of the load with the impedance of the source. 
However, the I-V characteristics of a solar panel make this task not so easy to accomplish. When looking at the I-V characteristics of a solar panel (Instert Picture) you can see that there is a point on the curve at which the Voltage and Current are both at their maximum. 
Since power in an electronic circuit is related by :math:`P=V\cdot I` you can see how having V at a maximum and I at a maximum creates the maximum amount of power. 
Unfortunately this only occurs at a certain load resistance. You also dicern from the I-V characteristic curve of a solar panel that if you were to deviate just slightly from that ideal resistance there would be a very large drop in the amount of power that is being produced. 
Usually however you are not so lucky with your load resistance as it can be changing constantly. What would work great is if there was a way to have a resistor that could be changed in order to constantly match this ideal resistance. If this were an AC circuit it could be done very easily with a transformer as a resistance seen across a transformer is described as :math:`R_p = N^2 \cdot R_s` where :math:`R_p` is the resistor on the primary side, :math:`R_s` is the resistor on the secondary side, and N is the turns ratio of the transformer. Unfortunately this is a DC circit and not an AC circuit.  

How Buck Converters are "DC Transformers"
----------------------------------------------
Transformers for DC circuits don't really exist. However, there is a very clever way of taking a DC source turning into AC and then back into DC all in one concise circuit. These circuits are called switching mode DC-to-DC converters. There exists many circuit topologies that are all based around the same concept of taking a DC signal converting it to AC then back to DC. Some of these circuit topologies are SEPIC, Cuk, Buck, Boost, and Buck-Boost. In this document we are only going to focus on Buck converters. This is because the output voltage of the solar panel is around 18V which will then need to be converted to 4.2V to charge the lipo battery. 

The Buck converter circuit topology is shown below. In all switching mode DC converters there is always a switch which will switch on and off at a given frequency :math:`f_s` with a given duty cycle represented by :math:`D`.
Usually, this switch is implemented by the use of MOSFET transistor where the gate is connected to a control signal that provides a squarewave at :math:`f_s` with the desired duty cycle. 
Now we can see how this duty cycle :math:`D` is actually analogous to the turns ratio of an AC circuit.

Starting the analysis by identifying two different states that the buck converter can be in. The first being when the switch is on and the second is when the switch is off. For this analysis we are going to treat the MOSFET as just a simple switch. 


.. figure:: Buck.svg
   :width: 400px
   :align: center
   :height: 200px
   :alt: Buck Converter
   :figclass: align center

   Buck Converter (*Wikipedia*, 2019)

.. figure:: Buck_Waves.png
   :width: 400px
   :align: center
   :height: 250px
   :alt: Waveforms
   :figclass: align center

   Waveforms of a Buck converter (*Wikipedia*, 2019)

There are great things with the maths and stuff
