To begin, it is best to start off with a sample script, to save you the trouble of having to establish the basic structure. I recommend taking the script for the Tatra tram, as it already includes all files and references necessary for a basic, movable train. As a basic requisit, I assume you already have either cloned the metrostroi beta repo, or that you've downloaded and extracted the Metrostroi script addon.

The scripts can be found in the extracted Metrostroi addon folder under ``lua/entities/gmod_subway_tatra_t3``.

Copy them into a new folder with the naming pattern ``gmod_subway_`` followed by whatever name you desire and make sure the folder you create sits in ``lua/entities``.

We also need to go and fetch its systems file. Go to ``lua/metrostroi/systems/`` and copy ``sys_tatra_systems.lua`` into the same folder you're taking it from. Rename it ``sys_`` followed by whatever name you choose.

Open the file in your preferred text editor (do NOT torture yourself by using a standard editor like Notepad, use a better one like Notepad++ or even VSCodium) and look for the line containing ``DefineSystem`` and change the string in the parentheses to anything you wish. It's probably best to make it relevant to your train though.

Next, to keep your train from erroring upon spawn, you need to go to the train script folder that you've created. Open shared.lua and look for a line containing ``LoadSystem``. Replace the String within the parentheses with whatever you named your system in the line containing ``DefineSystem``.

While we're in this file, feel free to change the name of your entity. You have to add a few instructions at the top in order to make that work. See [here](https://wiki.facepunch.com/gmod/Structures/ENT) for a listing of those. You may change the category, author name, entity name, etc to your liking.


If that's all done, you should now see your new entity in the entity browser under the category you gave it. Huzzah!
