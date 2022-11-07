# ScrollOfDebug
A scroll that dynamically detects and provides an interface to create classes for the game Shattered Pixel Dungeon and its mods while running the game.

Currently, the Scroll of Debug only works when ran on .jar versions of the game. It lacks the ability to detect files in the Android filesystem.

## Installation
1. Obtain a fork of <https://github.com/00-Evan/shattered-pixel-dungeon> that is updated to be at least consistent with [v1.0.0](https://github.com/00-Evan/shattered-pixel-dungeon/releases/tag/v1.0.0).

2. Add this repository.
````shell
git remote add ScrollOfDebug https://github.com/Inferno214221/ScrollOfDebug
git pull ScrollOfDebug shpd/1.2/pc-only
````
You'll be able to update the repository by calling `git pull ScrollOfDebug shpd/1.2/pc-only`.

3. Ensure the code compiles.
    * If the directory `shatteredpixel.shatteredpixeldungeon` was changed in the fork, a mass find and replace must be done for the scroll to work properly.

4. Make the scroll accessible in-game.
    * You can do this via [`add-automatically.patch`](https://github.com/Zrp200/ScrollOfDebug/blob/master/add-automatically.patch), which will add ScrollOfDebug to the correct location automatically and amend [`GameScene.java`](https://github.com/00-Evan/shattered-pixel-dungeon/blob/master/core/src/main/java/com/shatteredpixel/shatteredpixeldungeon/scenes/GameScene.java) to automatically place the Scroll of Debug into the hero's inventory when loading a game in INDEV mode.
    * Alternatively you can add some lines to HeroClass.java. Add: 
	````java
	import com.zrp200.scrollofdebug.ScrollOfDebug;
	````
	after the imports,
	````java
	if (SPDSettings.debugScroll()) initDebug(hero);
	````
	at the end of `initHero`, and add 
	````java
	private static void initDebug( Hero hero ) {
		ScrollOfDebug debug = new ScrollOfDebug();
		Dungeon.hero.belongings.backpack.items.add(debug);
		Dungeon.quickslot.setSlot(Dungeon.quickslot.SIZE - 1, debug);
	}
	```` 
	after `initHuntress`.

5. Enjoy!
