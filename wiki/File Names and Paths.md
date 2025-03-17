# Folders
``lua/entities/``
The default folder for scripted entities. It's not specific to Metrostroi, but anything you make that is a scripted entity goes here.

``lua/metrostroi``
The main folder of Metrostroi. Your vehicle scripts reference other scripts in this folder. The bare script files found in here are really not something you should edit, unless you have grand plans of forking Metrostroi itself.

``lua/metrostroi/systems``
This is the folder for train system simulations. Metrostroi prefers to modularise its scripts, so that different trains that have components in common can use one and the same script interchangeably. Turbostroi also hooks into these files specifically I believe, to speed up their execution. (Citation needed)

``lua/metrostroi/skins``
This one is self-explanatory I think. It contains the scripts that add skin entries to the train spawner. If you implement skin support in your train script correctly, you can write a script that adds alternative liveries to your train and put them here.

``lua/metrostroi/maps``
This folder contains scripts correlating to Metrostroi maps. They add announcers, destination boards, etc. Unless you make a map, you don't need to learn what they are in detail.

``lua/metrostroi_data``
Contains prerecorded track data for maps, and translations. You will only need to touch this once you create translations for your train.

And these are all the vaguely relevant folders of Metrostroi!

***   


# Files

``cl_init.lua`` and ``init.lua`` and ``shared.lua``
These are the main files of your entity. 

``cl_init`` is executed only on the client and is responsible for client-side things, like sounds, drawing and animating props, drawing lights , button arrays (called "panels") and corresponding buttons and anything to do with presenting the player the train, but not simulating its *inner* workings.

``init.lua`` is executed only on the server and represents part of the inner workings of the train. Not *all* of the inner workings as Metrostroi tries to be modular in its approach. Certain components are outsourced into system files, in order to speed up their processing with Turbostroi (citation needed), and to allow for different trains to share the same component and save on scripting said part redundantly.
Some of its functions include spawning the driver's seat, drawing lights, commanding the bogies according to whatever traction simulation setup there is (that's up to you to write), etc. If multiple system files are used, you could say it brings all the different systems together. 

``shared.lua`` is executed both on server and client. That's why you should specify whether certain block of code in this file should be executed on client or server (if said code block is 'realm specific'). You can do it by supplying an 'if' condition with keyword CLIENT or SERVER as a boolean expression so the certain code block will be executed only on a client or a server respectively. 
Usually contains info on the author, which category to list the entity in, whether it's admin spawnable, etc. On those, see [here](https://wiki.facepunch.com/gmod/Structures/ENT).
In our case, it contains definitions for the standing area for passengers, door positions, announcer positions if applicable (you will likely code your own announcer system), camera positions, the function containing sound definitions with positioning, information on the car for the train spawner, the car's possible randomly generated car number range.


``sys_***.lua``
This is the file that simulates a certain system that you define. Whether that be a simulation of a battery, air horn, a group of circuits for whatever function you think needs to be accelerated by Turbostroi (but not necessary; you can define whether your system to be accelerated by Turbostroi or not by supplying 'TRAIN_SYSTEM.DontAccelerateSimulation = true' flag at the beginning of the file), etc. I recommend looking at the files that come with Metrostroi, to get a sense of what range of things have been implemented in this file Project Light Rail has proceeded to put most core train logic into the systems file, while minor but still important things are kept in the init.lua file. The design considerations of this are up to you. A systems file is more easily swapped out than a full entity script, allowing for quicker overhauls.
