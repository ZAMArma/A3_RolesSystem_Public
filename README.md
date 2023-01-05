# Arma 3 Roles System Version 1.1.0

<p align="center">
  <a href="https://discord.gg/W4ew5HP">
    <img src="https://img.shields.io/discord/700228330959536190?color=7683D5&label=Discord&logo=What&style=flat-square" alt="ZAM Discord">
  </a>
</p>

## Overview

ZAM’s Roles System (RS) was designed to incentivize teamplay and coordination between those in groups together. You will be (practically) forced to join a group with others as if you are alone you will be forced as a ‘Recruit’ role which has poor weaponry, no access to the arsenal, and limited ammo. You can change your role by pressing **Ctrl + 8**.

## Roles Breakdown

Joining a group gives you access to all basic roles: Rifleman, Medic (two max), Crewman, Pilots, and Squad Leader. 
The Specialist roles are unlocked once a group has 5 members (two max): Autorifleman, Light Anti-Tank, Marksman, and Grenadier. 
The Support roles are unlocked when the group has 7 members (one max): Heavy Gunner, Heavy Anti-Tank, and Sniper. 

## Role Limitations

Depending on your role you will be limited to certain equipment and weapons. In addition, if you are not a crewman or pilot role you cannot enter the respective vehicles as a crewmember. You can carry extra mags for your teammates who have different roles, however, you cannot pick up their weapons.

## Ground Commanders

Ground Commanders are selected by the players via a vote. They have access to supports, and when they are selected, are the only ones able to speak in Global and Side chat.

**To start a vote:**
```sqf
[timeForVotingInSeconds,side] spawn MAZ_RS_fnc_startCommanderVote;
```

**To manually add a commander:**
```sqf
[unit,side] call MAZ_RS_fnc_addCommander;
```

**To remove a commander:**
```sqf
[side] call MAZ_RS_fnc_removeCommander;
```

# Roles System Equipment Configuration Tutorial

## General Information

**Warning:**

When creating a new equipment configuration you _MUST_ create role setups for each of the roles below.

If you don't create one for a role they will have nothing available in their arsenal and will be able to pickup _ANY_ items.
```sqf
'Recruit', 
'Rifleman', 
'Medic', 
'Crewman', 
'Heli Pilot', 
'Pilot', 
'Squad Leader', 
'Autorifleman', 
'Light Anti-Tank', 
'Marksman', 
'Grenadier', 
'Heavy Gunner', 
'Heavy Anti-Tank', 
'Sniper'
```

**Changing Configs**

To change the config for your downloaded version of the Roles System, copy and paste the contents of one of the config files into the function **MAZ_RS_fnc_createRoleEquipment**. 

**Creating Configs**

The most efficient way of creating new configs is to put all the items you want different roles to have in the virtual storage of a Huron Cargo Container in the editor then use the code below to get the items and sort them into the appropriate arrays. After you create the default uniform for most roles you only need to add weapons, it does not take very long.
```sqf
copyToClipboard str (cursorObject call BIS_fnc_getVirtualWeaponCargo);
copyToClipboard str (cursorObject call BIS_fnc_getVirtualItemCargo);
copyToClipboard str (cursorObject call BIS_fnc_getVirtualBackpackCargo);
copyToClipboard str (cursorObject call BIS_fnc_getVirtualMagazineCargo);
```

## Function Information

**MAZ_RS_fnc_createNewDefaultSideUniform**

The purpose of this function is primarily to reduce the workload on the config creator.<br/>
These defaults can be ignored in individual roles.<br/>
Calling this creates the following default items for the faction on the specified map:
```
- Uniforms
- Vests
- Backpacks
- Headgear
- Goggles
```

**Format:**

```sqf
[
	Side, (west, east, independent)
	MapName, ('Altis','Stratis','Enoch','Tanoa','Malden')
	[Uniforms Array], (Any uniform class names available to this side on the map)
	[Vests Array], (Any vest class names available to this side on the map)
	[Backpacks Array], (Any backpack class names available to this side on the map)
	[Helmets Array], (Any helmet class names available to this side on the map)
	[Goggles Array] (Any goggle class names available to this side on the map)
] call MAZ_RS_fnc_createNewDefaultSideUniform;
```

**MAZ_RS_fnc_createNewEquipmentForRole**

Calling this creates the role equipment for the specific role.<br/>
This includes the weapons, attachments, additional uniform items, additional items (LaserDesignator, Rangefinder, Medikit, Toolkit).

**Format:**
```sqf
[
	Side, (west, east, independent)
	MapName, ('Altis','Stratis','Enoch','Tanoa','Malden')
	Role, (Any of the strings in roles list above. CaSe-SeNsItIvE)
	[
		[
			[Primary Weapon Classes], (Any classnames for primary weapons)
			[Primary Mag Classes] (Any classnames for primary weapon magazines)
		],
		[
			[Launcher Weapon Classes], (Any classnames for launcher weapons)
			[Launcher Mag Classes] (Any classnames for launcher weapon magazines)
		],
		[
			[Pistol Weapon Classes], (Any classnames for pistol weapons)
			[Pistol Mag Classes] (Any classnames for pistol weapon magazines)
		],
		[Attachments] (Any classnames for attachments)
	],
	[Uniforms Array], (Any uniform class names available to this specific role)
	[Vests Array], (Any vest class names available to this specific role)
	[Backpacks Array], (Any backpack class names available to this specific role)
	[Helmets Array], (Any helmet class names available to this specific role)
	[Goggles Array], (Any goggle class names available to this specific role)
	[Extra Items Array], (Any extra item class names available to this specific role)
	Use Default Uniforms? (TRUE / FALSE. 
				Whether to include the default uniform defined in MAZ_fnc_createNewDefaultSideUniform. 
				If not they will only have what is defined in above.
			      )
] call MAZ_RS_fnc_createNewEquipmentForRole;
```

## Examples of Function Calls

**MAZ_RS_fnc_createNewDefaultSideUniform**
```sqf
[
	west,
	"Altis",
	[
		"U_B_CombatUniform_mcam","U_B_CombatUniform_mcam_tshirt","U_B_CombatUniform_mcam_vest","U_B_CombatUniform_mcam_worn","U_B_CTRG_1","U_B_CTRG_2","U_B_CTRG_3","U_B_survival_uniform","U_I_G_Story_Protagonist_F","U_B_CTRG_Soldier_2_Arid_F"
	],
	[
		"V_PlateCarrier1_rgr","V_PlateCarrier2_rgr","V_Chestrig_oli","V_TacVest_khk","V_TacVest_oli","V_PlateCarrier_Kerry","V_PlateCarrierL_CTRG","V_PlateCarrierH_CTRG"
	],
	[
		"B_AssaultPack_rgr"
	],
	[
		"H_HelmetB","H_HelmetB_camo","H_HelmetB_light","H_Booniehat_khk","H_Booniehat_mcamo","H_Booniehat_tan","H_Booniehat_khk_hs","H_HelmetB_grass","H_HelmetB_snakeskin","H_HelmetB_desert","H_HelmetB_black","H_HelmetB_sand","H_Cap_oli","H_Cap_headphones","H_Cap_tan","H_Cap_blk","H_Cap_tan_specops_US","H_Cap_khaki_specops_UK","H_Cap_grn","H_Cap_oli_hs","H_Cap_usblack","H_MilCap_mcamo","H_MilCap_gry","H_HelmetB_light_grass","H_HelmetB_light_snakeskin","H_HelmetB_light_desert","H_HelmetB_light_black","H_HelmetB_light_sand","H_Bandanna_khk","H_Bandanna_khk_hs","H_Bandanna_cbr","H_Bandanna_sand","H_Bandanna_gry","H_Bandanna_mcamo","H_Watchcap_blk","H_Watchcap_cbr","H_Watchcap_khk","H_Watchcap_camo","H_Booniehat_mgrn","H_MilCap_grn"
	],
	[
		"G_Spectacles","G_Spectacles_Tinted","G_Combat","G_Shades_Black","G_Shades_Green","G_Shades_Red","G_Tactical_Black","G_Bandanna_blk","G_Bandanna_oli","G_Bandanna_khk","G_Bandanna_tan","G_Shades_Blue","G_Tactical_Clear","G_AirPurifyingRespirator_01_F"
	]
] call MAZ_RS_fnc_createNewDefaultSideUniform;
```

**MAZ_RS_fnc_createNewEquipmentForRole**
```sqf
[
	west,
	"Altis",
	"Rifleman",
	[
		[
			["arifle_MX_F","arifle_MX_Black_F","arifle_SPAR_01_blk_F","arifle_SPAR_01_snd_F"],
			["30Rnd_556x45_Stanag","30Rnd_556x45_Stanag_Tracer_Yellow","30Rnd_556x45_Stanag_Sand","30Rnd_556x45_Stanag_Sand_Tracer_Yellow","30Rnd_65x39_caseless_mag","30Rnd_65x39_caseless_black_mag","30Rnd_65x39_caseless_mag_Tracer","30Rnd_65x39_caseless_black_mag_Tracer"]
		],
		[
			[],
			[]
		],
		[
			["hgun_P07_F","hgun_Pistol_heavy_01_F","hgun_P07_blk_F"],
			["16Rnd_9x21_Mag","16Rnd_9x21_green_Mag","11Rnd_45ACP_Mag"]
		],
		["optic_Aco","optic_ACO_grn","optic_Holosight","acc_flashlight","acc_flashlight_smg_01","acc_pointer_IR","optic_Holosight_blk_F"]
	],
	[],
	[],
	[],
	[],
	[],
	[],
	true
] call MAZ_RS_fnc_createNewEquipmentForRole;
```
