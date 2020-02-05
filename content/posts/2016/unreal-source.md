---
layout: post
title:  "unreal source"
date:   2016-10-25 09:51:02
categories: unreal
---

## unreal

[Origin](https://docs.unrealengine.com/latest/INT/Programming/index.html)

#### Actors are instances of classes that derive from the AActor class;

#### Objects are instances of classes that inherit from the UObject class;

#### UObject:the base class of all objects in Unreal Engine, including Actors.

#### Actors can be thought of as whole items or entities, while Objects are more specialized parts.

#### gameplay classes such as GameMode, GameState, and PlayerState set the rules of the game

-------------------------

#### A Pawn is an Actor that can be an "agent" within the world.

#### A Character is a humanoid-style Pawn.

#### A Controller is an Actor that is responsible for directing a Pawn.

-------------------------
#### A HUD is a "heads-up display", or the 2D on-screen display that is common in many games.

#### The PlayerCameraManager is the "eyeball" for a player and manages how it behaves.

-------------------------
#### GameMode is the definition of the game, including things like the game rules and win conditions. It only exists on the server.

#### GameState contains the state of the game, which could include things like the list of connected players, the score

-------------------------

#### Unreal Motion Graphics (UMG)

UMG = lots of widgets
Unreal Motion Graphics UI Designer (UMG) is a visual UI authoring tool which can be used to create UI elements such as in-game HUDs, menus or other interface related graphics you wish to present to your users. At the core of UMG are Widgets, which are a series of pre-made functions that can be used to construct your interface (things like buttons, checkboxes, sliders, progress bars, etc.). These Widgets are edited in a specialized Widget Blueprint, which uses two tabs for construction: the Designer tab allows for the visual layout of the interface and basic functions while the Graph tab provides the functionality behind the Widgets used.

-------------------------

## 实际使用BP


### 获取socket.io的插件后，直接按照教程就可以和web页进行通讯了，整体比较简单

### 想要进行远程控制，尝试模拟远程控制器，球体这边有个关键的概念叫做Torque，是用来控制扭矩的，一直按着会增加扭矩，松开会不变，反方向同样
