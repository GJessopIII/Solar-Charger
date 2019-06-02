Maximum Power Point Tracking (MPPT)
===================================

Maximum Power Point Tracking (MPPT) uses the well know fact that in order to extract the maximum power from a source you must match the impedance of the load with the impedance of the source. 
However, the I-V characteristics of a solar panel make this task not so easy to accomplish. When looking at the I-V characteristics of a solar panel (Instert Picture) you can see that there is a point on the curve at which the Voltage and Current are both at their maximum. 
Since power in an electronic circuit is related by :math:`P=V\cdot I` you can see how having V at a maximum and I at a maximum creates the maximum amount of power. 
Unfortunately this only occurs at a certain load resistance. You also dicern from the I-V characteristic curve of a solar panel that if you were to deviate just slightly from that ideal resistance there would be a very large drop in the amount of power that is being produced. 
Usually however you are not so lucky with your load resistance as it can be changing constantly. What would work great is if there was a way to have a resistor that could be changed in order to constantly match this ideal resistance. If this were an AC circuit it could be done very easily with a transformer as a resistance seen across a transformer is described as :math:`R_p = N^2 \cdot R_s` where :math:`R_p` is the resistor on the primary side, :math:`R_s` is the resistor on the secondary side, and N is the turns ratio of the transformer. Unfortunately this is a DC circit and not an AC circuit.  

How Buck Converters are "DC Transformers"
----------------------------------------------
Here I am going to show mathematically how a Buck Converter can be used as a "DC transformer".

