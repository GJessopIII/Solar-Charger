.. Solar-Charger documentation master file, created by
   sphinx-quickstart on Thu May 23 01:05:27 2019.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome!
=========================================
This project was proposed to the Power Electronics class at Walla Walla University (ENGR 460). Since we had been studying DC-DC buck/boost converters our professor Dr. Rob Frohne gave us a cheap 2.5W solar array and tasked us with drawing maximum power from the array using Maximum Power Point Tracking (MPPT). All files referenced for this project are located at on the `Repository <https://github.com/cosgais/Solar-Charger>`_. 


Specifications
==============

Some specifications that where established was that it must use MPPT tracking and it must charge a phone. How this was accomplished was interpreted in different ways. For me I used MPPT to charge a battery which then was sent through a boost converter to then charge my phone. For others they chose to use an arduino to measure the values and attempt to implement the MPPT themselves with an arduino. If you are unsure what MPPT tracking is see the section on it in the table of contents below. My design was based on the principles explained in the MPPT section however, since there already existed IC's out there that would do the functions I needed I just understood how the IC worked and did not implement MPPT myself. 


Contents:
=========

.. toctree::
   :maxdepth: 2
   
   mppt
   circuit
   troubleshooting


