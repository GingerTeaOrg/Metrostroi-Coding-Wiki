#  cl_init.lua




## ENT:Animate(clientProp, value, min, max, speed, damping, stickyness)
Animates a prop according to its hardcoded pose parameters. The pose parameter needs to have the name "position" defined in the model's qc file.

> `clientProp`:Name of the prop to be animated, defined in ENT.ClientProp.   
> `value`: Percentage of pose parameter. Can be static integer or name of a variable. Obviously the latter should be used.   
> `min`: minimum value of the pose parameter as defined in qc   
> `max`: maximum value of the pose parameter as defined in qc   
> `speed`: How quickly the animation should try to follow the animation change. It's best to play around with this value, in order to ascertain what speed looks most natural.   
> `damping`: TODO: Find out.   
> `stickyness`: TODO: Find out.    







## function ENT:AnimateFrom(clientProp,from,min,max)

TODO: Find out what it does. Never used it before or seen it used.





## function ENT:CreateRT(name, w, h)

Create a rectangle of a certain dimension. Used for things like the LCD screens.

> `name`: Name of the rectangle object   
> `w`: Width   
> `h`: height   





## function ENT:DrawDigit(cx,cy,digit,scalex,scaley,thickness)

This seems to draw a segment display number. Probably used on those trains with a segmented display.   

> TODO   







## function ENT:DrawOnPanel(index,func,overr)   

> TODO   




## function ENT:DrawRTOnPanel(index,rt,overr)   

> TODO



## self:DrawOnPanel(index,func,overr)

Internal function for drawing something onto a panel. Can presumably be used to develop your own functions that could do some arbitrary 2D rendering.



## self:DrawSchedule(panel)

Draws a schedule table on a given ``panel``. Currently unused.




## self:GetNW2Int("name", fallback_value_int)

Same as `self:GetNWInt`. Reads a networked integer from the server, if the NW2Int was called by a server script. If a clienside script defined the NW2Int, it can only be read clientside. If it was defined serverside, both client and server scripts can read from it. Read about the intricacies [here](https://wiki.facepunch.com/gmod/Entity:SetNWInt).



## self:GetPackedBool("name", fallback_value_bool)

 Same as [this](https://wiki.facepunch.com/gmod/Entity:GetNWBool). Sometimes used in place of the original function for _whatever reason_.



## self:HideButton(clientProp, value)

 Presumably hides a button. Could be useful in certain situations. Untested by the author.



## self:HidePanel(kp,hide)

Hides a given panel in `kp`. Set the second argument `hide` to a boolean. Could presumably be used in cases like a circuit breaker panel that hides breaker switches, so only if it's opened shall the panel be visible.



## self:PlayOnce(soundid,location,range,pitch,randoff)

Plays an unlooped given sound by name. Make sure it is only triggered once for one tick, otherwise the sound will restart every tick, constantly interrupting itself. Ie only use this in conjunction with a function that only triggers once.

> `soundid`: sound name you defined in shared.lua. If the passed argument is a table array, it will choose randomly from the list of sounds you pass.

> `location`: Valid string values are "cab", "instructor", "front_bogey", "read_bogey". Leave unset if you don't want to have the sound play in a certain location.

> `range`: Self-explanatory. Experiment with the audible range until it sounds right. For some reason, the default range of 0.50 is hardcoded for when the sound name is "switch".

> `randoff`: Disable range randomisation. You can omit this argument if you don't want to do this.



## self:SetLightPower(index,power,brightness)

Turns a preset light on and off.

> `index`: Light index number that you defined in your lights array
> `power`: On or off, accepts a boolean argument
> `brightness`: Manually define a brightness



## self:SetNW2Int

Same as [this](https://wiki.facepunch.com/gmod/Entity:SetNWInt). Actually there is slight difference between SetNW.. and SetNW2.. functions. SetNW.. makes the network variable to be broascasted every 10 seconds, while SetNW2.. broadcasts it only once when the variable's value has been changed



## self:SetSoundState(sound,volume,pitch,timeout,range)

Enables a looped sound.

> `sound`: The sound name

> `volume`: well, duuh

> `pitch`: *blows raspberry*

> `timeout`: Disables the sound after given seconds? (Citation needed)

> `range`: Range of the sound. Same as the argument on PlayOnce.

## self:ShowHide(clientProp, value)

 Hide or show given client prop. First argument is the name of the prop you've given it in a ClientProp entry, second is a boolean. Can naturally be used in conjunction with a boolean variable as an input.

## self:ShowHideSmooth(clientProp, value)

 Smoothly hides or shows a client prop. Could be useful for things like smoothly fading in the prop that goes in front of your headlights, to simulate the lights being toggled. Same as its instant counterpart.

## self:ShowHideSmoothFrom

> TODO


## self:UpdateTextures()

Forces the entity to update its textures. Useful if for whatever reason, skins aren't being applied.



#  init.lua

## self:SetModel("modelname")

Set model according to path that you pass as string, ie ``"models/lilly/uf/u2/u2h.mdl"``. Occurs in ``function ENT:Initialize()``. See your example script that you copied in "Getting Started".

## function ENT:TrainSpawnerUpdate()

Sets the parameters for the train spawner.

Example: 

```lua
function ENT:TrainSpawnerUpdate()
			
		
        self.FrontCouple:SetParameters() --get the coupler type from the variable
        self.RearCouple:SetParameters()
		local tex = "Def_U2"
		self:UpdateTextures()
		--self:UpdateLampsColors()
		self.FrontCouple.CoupleType = "U2" --ensures the couplers are the correct model`
		self.RearCouple.CoupleType = "U2"
end
```

## self:WriteTrainWire(num,value)

Write to a train wire that will be available across all coupled units. This is your ticket to Multiple Unit operation. Expects an integer for `value`. I recommend keeping an excel sheet or txt somewhere that notes which wire number does what, because Metrostroi is sure as shite not going to tell you.

## self:ReadTrainWire(num)

Read from a given train wire.

## self.System_Name:TriggerInput(name,value)

Writes a value to a system's input.

## ENT:OnButtonPress(button,ply)

This function assigns actions to the button names defined in the keymap. More on that on the page for buttons.

## ENT:OnButtonRelease(button,ply)

This function sets an action for when a given button is released. Useful for buttons that cause an action for as long as they are held down, ie deadman's pedal. More on that on the buttons page.



#  shared.lua

## ENT.SkinType

Accepts a string value. Set this to whatever name you're using in the skin registry script.

## function ENT:PassengerCapacity()

Tells Metrostroi how many passengers your vehicle can accept. I'd recommend making this dependant on standing area.

```lua
function ENT:PassengerCapacity()
    return 81
end
```

## ENT:GetStandingArea()

Defines the area where passengers stand. Defined as Vector starting at xyz, ending at vector xyz. Experiment, or find out the rough coordinates from your Model in Blender.

```lua
function ENT:GetStandingArea()
    return Vector(465,-20,35),Vector(60,20,35)
end
```

## ENT:InitializeSounds()

Defines sounds by name, position, how long their loop is, etc. More on the sounds page.

```lua
function ENT:InitializeSounds()
	self.BaseClass.InitializeSounds(self)
	self.SoundNames["bell"] = {loop=0.01,"lilly/uf/u2/Bell_start.mp3","lilly/uf/u2/Bell_loop.mp3", "lilly/uf/u2/Bell_end.mp3"}
	self.SoundPositions["bell"] = {1100,1e9,Vector(386,-20,8),0.7}
	self.SoundNames["Startup"] = {"lilly/uf/u2/startup.mp3"}
	self.SoundPositions["Startup"] = {800,1e9,Vector(550,0,55),1}
end
```

## ENT.LeftDoorPositions = {} and ENT.RightDoorPositions = {}

This is an array defining where the doors are. Values are defined as Array(x,y,z). If your train doesn't have doors that always open, you could create a function that randomises which doors are inserted into the table during boarding, so that passengers only board the doors that you visually open.

## ENT.Cameras = {}

This is an array for defining where the cameras for the SHIFT + arrow keys are and what they're called. Accepts Vector coordinates and angles.

```lua
ENT.Cameras = {
    {Vector(480.5+17,-40,110),Angle(0,-90,0),"Train.UF_U2.Destinations"},
    {Vector(407.5+10,6,100),Angle(0,180+5,0),"Train.UF_U2.PassengerStanding"},
	{Vector(70.5+10,6,100),Angle(0,0,0),"Train.UF_U2.PassengerStanding2"},
    {Vector(490.5+90,0,150),Angle(0,180,0),"Train.Common.RouteNumber"},
    {Vector(570,0,70),Angle(80,0,0),"Train.Common.CouplerCamera"},
}
```

## ENT.MirrorCameras

Array for the mirror cameras.

```lua
ENT.MirrorCams = {
    {Vector(407.5+30,40,5) ,Angle(30,10,0),"Train.U2.Left"},
    {Vector(450+13,0,26),Angle(60,0,0),"Train.U2.Right"},
}
```

## function ENT:InitializeSystems

Tells the train which systems to load.

```lua
function ENT:InitializeSystems()
	self:LoadSystem("Duewag_U2")
	self:LoadSystem("Duewag_Deadman")
	self:LoadSystem("IBIS")
	self:LoadSystem("Duewag_Battery")
	--self:LoadSystem("duewag_electric")
end
```

## ENT.SubwayTrain

Information for the train spawner on the car. Pretty self-explanatiory. Metrostroi trains have got some extra information like ARS, electrical coupling type, etc. But those are probably not relevant for you, unless you're coding a Russian Metro train that supports these systems. This is the minimum version:

```lua
ENT.SubwayTrain = {
	Type = "U2",
	Name = "U2h",
	WagType = 0, --zero for trailer or head, 1 for only head, 2 for only trailer
	Manufacturer = "Duewag",
}
```
