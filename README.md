# qb-erpitems

* Adds useless ERP items to your roleplay server.

# Future updates.

* I may add more items feel free to PR

# Installation

**qb-inventory/html/images.lua**
**Drag and drop the images into the image folder**

**qb-core/shared/items.lua**
**Add these items to your qb-core items.lua**

```lua
	-- MUZZYs ERP Items
	["vcard"] 				= {["name"] = "vcard", 					["label"] = "V-Card", 			["weight"] = 1000, 		["type"] = "item", 		["image"] = "vcard.png", 		["unique"] = false, 	["useable"] = true, 	["shouldClose"] = true, 	["combinable"] = nil, 	["description"] = "A card that holds someones virginity."},
	["vibrator"] 				= {["name"] = "vibrator", 					["label"] = "Pink Vibrator", 			["weight"] = 1000, 		["type"] = "item", 		["image"] = "vibrator.png", 		["unique"] = false, 	["useable"] = true, 	["shouldClose"] = true, 	["combinable"] = nil, 	["description"] = "A powerful drill."},
	["condom"] 				= {["name"] = "condom", 					["label"] = "Durex Condom", 			["weight"] = 1000, 		["type"] = "item", 		["image"] = "condom.png", 		["unique"] = false, 	["useable"] = true, 	["shouldClose"] = true, 	["combinable"] = nil, 	["description"] = "Protects your money from child support."},
```

**Add to qb-shops (location is set for gabz map)

**qb-shops/config.lua**
**Add this to Config.Products**

```lua
["vu"] = {
        [1] = {
            name = "condom",
            price = 2,
            amount = 50,
            info = {},
            type = "item",
            slot = 1,
        },
		[2] = {
            name = "vibrator",
            price = 50,
            amount = 50,
            info = {},
            type = "item",
            slot = 2,
        },
		[3] = {
            name = "vcard",
            price = 15,
            amount = 50,
            info = {},
            type = "item",
            slot = 3,
        },
    },
```

**qb-shops/config.lua**
**Add this to Config.Locations**

```lua
--Vanilla Unicorn
	["vu"] = {
        ["label"] = "Vanilla Unicorn",
        ["coords"] = vector4(132.82, -1293.78, 29.27, 120.37),
        ["ped"] = 'mp_f_stripperlite',
        ["scenario"] = "WORLD_HUMAN_PROSTITUTE_HIGH_CLASS",
        ["radius"] = 1.5,
        ["targetIcon"] = "fas fa-shopping-basket",
        ["targetLabel"] = "Open Sex Store",
        ["products"] = Config.Products["vu"],
        ["showblip"] = false,
        ["blipsprite"] = 110,
        ["blipscale"] = 0.6,
        ["blipcolor"] = 0,
    },
```

## Add to DPEmotes
```lua
   ["Cuddle1"] = {"cuddlepartner1@pawuk", "cuddlepartner1_clip", "Cuddle1", AnimationOptions =
   {
	   EmoteLoop = true,
       EmoteMoving = false,
   }},
   ["Cuddle2"] = {"cuddlepartner2@pawuk", "cuddlepartner2_clip", "Cuddle2", AnimationOptions =
   {
	   EmoteLoop = true,
       EmoteMoving = false,
   }},

```

## Add to qb-smallresources/client/consumables.lua
```lua
RegisterNetEvent('consumables:client:UseVibrator', function(itemName)
    TriggerEvent('animations:client:EmoteCommandStart', {"Cuddle1"})
    SEVENCore.Functions.Progressbar("vibrator_sex", Lang:t('consumables.vibrator'), 50000, false, true, {
        disableMovement = false,
                disableCarMovement = false,
                disableMouse = false,
                disableCombat = true,
            }, {
                animDict = "cuddlepartner1@pawuk",
                anim = "loop",
                flags = 49,
            }, {}, {}, function() -- Done
        TriggerEvent("inventory:client:ItemBox", SEVENCore.Shared.Items["vibrator"], "remove")
        SEVENCore.Functions.Notify("Your clit is feeling amazing!", "success")
        TriggerEvent('animations:client:EmoteCommandStart', {"c"})
        TriggerServerEvent('hud:server:RelieveStress', math.random(2, 4))
    end)
end)
```

## Add to qb-smallresources/server/consumables.lua
```lua
SEVENCore.Functions.CreateUseableItem("vibrator", function(source)
    TriggerClientEvent("consumables:client:UseVibrator", source, true)
end)
```