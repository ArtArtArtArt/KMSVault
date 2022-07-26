# Unreal from launch to begin play

https://www.youtube.com/watch?v=IaU2Hue-ApI&t=1s&ab_channel=AlexForsythe

 - Launch module starts everything

## PreInit
![[Pasted image 20220725203407.png]]

Most of plugins are loaded here

![[Pasted image 20220725203532.png]]

When the module is loaded 
 - The system registers all UObjects defined in a module
 - CDO is constructed (class default state) - this will later be passed to a UCLASS constructor (const FObjectInitializer& ObjectInitializer) - so no gameplay related code here
 - ModuleStartup is called

## Init 
![[Pasted image 20220725204050.png]]
![[Pasted image 20220725204311.png]]
UEngine is either game or editor engine. It is responsible for loading the default map. 
![[Pasted image 20220725204410.png]]

### Engine init
![[Pasted image 20220725204536.png]]

![[Pasted image 20220725204623.png]]
These are the entities that are initialized when engine is started
![[Pasted image 20220725204658.png]]

### Engine start

![[Pasted image 20220725205006.png]]
Before and after load map objects have different lifespan - game object live as long as map is loaded

![[Pasted image 20220725204818.png]]

Here is how world and level are interconnected
![[Pasted image 20220725205131.png]]
**This all goes to UPackage** - .umap file

First part of world loading
![[Pasted image 20220725205338.png]]
![[Pasted image 20220725205412.png]]

After that 
![[Pasted image 20220725205551.png]]
(Add To Root prevents the world from being garbage collected)

#### Initialize actors for play
![[Pasted image 20220725205652.png]]

![[Pasted image 20220725205818.png]]
Which does the following thing inside
![[Pasted image 20220725205905.png]]

Also if it is a primitive component - proxy is created and added to the scene (which is render thread version of a world)

After that Actors are in this state
![[Pasted image 20220725210101.png]]

### Init game function

![[Pasted image 20220725210128.png]]

which spawns gameSessionActor
![[Pasted image 20220725210208.png]]

### Initialize actors for play

![[Pasted image 20220725210313.png]]

This happens in two passes
![[Pasted image 20220725210426.png]]
Here components can initialize themselves before the components
Also a lot of additional stuff is initialized here
![[Pasted image 20220725210526.png]]

The second loop calls these
![[Pasted image 20220725210607.png]]

Initialize components in more details
![[Pasted image 20220725210712.png]]
![[Pasted image 20220725210739.png]]

### After the world is initialized
You have these objects
![[Pasted image 20220725210852.png]]

*STOPPED AT 14:16 https://www.youtube.com/watch?v=IaU2Hue-ApI&t=1s&ab_channel=AlexForsythe*




---
status: #⚙️ 
tags: 
related: 
