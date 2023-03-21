# Basic Phaser Editor 2D script nodes

This project contains a couple of Script Nodes for Phaser Editor 2D.

These script nodes are very basic and may fit on any Phaser Editor 2D project.

The scripts are coded in TypeScript with ES modules.

## Installing

Copy this project folder (or clone the repo) and paste it into your project's `src/` folder.

## Summary

There are three groups of scripts: **Base**, **Triggers**, and **Actions**.

### Base scripts

Contain basic/abstract functionallity. Often, you will create prefab variants of them (extend them).

* **ScriptNode** - the base class for all the scripts.
* **SpriteScriptNode** - base prefab for script nodes accessing sprite objects.

### Trigger scripts

These scripts listen certain event. When the event is triggered, then execute the children, which are actions.

* **OnEventScript** - listens the given `eventName` object's event.
* **OnKeyboardEventScript** - listens the given `eventName` keyboard's event.
* **OnPointerDownScript** - a prefab variant of **OnEventScript**, listening the `pointerdown` event.
* **OnSceneAwakeScript** - listens the `scene-awake` event of the scene.

### Action scripts

Actions are script that are executed manually or by other nodes, like triggers or other actions.

* **CallbackActionScript** - executes the given `callback` expression.
* **StartSceneActionScript** - starts the given `sceneKey` scene.
* **ExecActionScript** - executes the given `targetAction`.

## ScriptNode

The base of all the scripts. Probably it is already avaliable in your project (if you generated it with Phaser Editor 2D).

This class provides methods for managing the node's children, and implementing the scene events: `awake`, `start`, and `update`.

## SpriteScriptNode

A base script for all the scripts accesing sprite objects. It just overrides the `gameObject` property and set its type to `Phaser.GameObjects.Sprite`. This helps IDE auto-completion and type-checking.

## OnEventScript

A trigger-like script node. It listens the given `eventName` of the game object and executes the children action nodes. 

You can create handy prefab variants for different events, like the `OnPointerDownScript` prefab.

## OnKeyboardEventScript

A trigger-like script node. It listens the given `eventName` on the keyboard plugin, and executes the children action nodes.

An example of `eventName` values could be `keydown-SPACE`, `keyup-LEFT`, `keydown-W`... It follows the same syntax of the KeyboardPlugin events (`scene.input.keyboard.on(...)`).

## OnPointerDownScript

A trigger-like script. It is a prefab variant of the `OnEventScript` node. It listens to the `pointerdown` event of the game object, and executes the children action nodes.

If the game object's input is not set whe the scene "awakes", then this script calls the `gameObject.setInteractive()` method.

## OnSceneAwakeScript

A trigger-like script. It listens the `scene-awake` event of the scene, and executes the children action nodes.

## CallbackActionScript

An action-like script. It executes the given `callback` expression. You can use this script for executing custom methods from your prefabs or scenes.

## StartSceneActionScript

An action-like script. It starts the given `sceneKey` scene.

## ExecActionScript

An action-like script. It executes the given `targetAction`. You can use this script for executing an action node from script-tree.

For example, let's say you have a **JumpAction** for jumping a character. But you want to call this action when different events are fired:

- When you click a jump button.
- When you press the `SPACE` key.
- When you press the `UP` button of an external gamepad.

So, you can use different **ExecActionScript** nodes in different contexts, but referencing the same **JumpAction** node.
