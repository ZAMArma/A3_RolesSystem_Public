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
