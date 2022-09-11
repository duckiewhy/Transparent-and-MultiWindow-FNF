# Transparent-and-MultiWindow-FNF

Yeah! This is the code for transparent windows and mutliple linked windows for FNF code. This can also be used for other stuff, but this is a template for FNF code.

THIS ISN'T IN LUA!! ITS HARDCODED (in psych engine) !!!!!!!!!!!!!

## Credits:
* [DuskieWhy] (https://twitter.com/DuskieWhy)
* [TaeYai] (https://twitter.com/TaeYai)
* [BreezyMelee] (https://twitter.com/BreezyMelee)
* [YoshiCrafter] (https://twitter.com/YoshiCrafter29) - Additional help
* [KadeDev] (https://twitter.com/kade0912) - Transparent window .hx file code

# Transparent windows 
First off, import the FlxTransWindow.hx from this repository.
Next, you are going to want to make a bg sprite like this:

```
var bg:FlxSprite = new FlxSprite().makeGraphic(FlxG.width, FlxG.height, FlxColor.fromRGB(1, 1, 1));
if (defaultCamZoom < 1)
{
  bg.scale.scale(1 / defaultCamZoom);
}
bg.scrollFactor.set();
add(bg);
```
Then, afterwards, put the line 
```FlxTransWindow.getWindowsTransparent();```
directly below it.
This will make the sprite of bg, and everything below it, transparent!
You can add sprites above it to hide it, and toggle the visibility to reveal the transparent window.

### WARNING: ANY PIXELS WITH AN ALPHA BELOW ONE WILL HAVE BLACK BELOW IT, LIKE IMAGE 1


I recommend adding a sprite below, or removing any transparent pixels and fixing them up. 
Like image 2!

![](https://albumizr.com/ia/8c5415605f8d9fb6093971ffa0281c05.jpg)

![](https://cdn.discordapp.com/attachments/884274552295792732/1018398012575322112/unknown.png)

# Multi-Window
We are going to make this window just create the dad. The rest, you're on your own!

First, in PlayState.hx, you are going to want to import all of this:

```
import lime.app.Application;
import lime.graphics.RenderContext;
import lime.ui.MouseButton;
import lime.ui.KeyCode;
import lime.ui.KeyModifier;
import lime.ui.Window;
import openfl.geom.Matrix;
import openfl.geom.Rectangle;
import openfl.display.Sprite;
import openfl.utils.Assets;
```

Define these variables:

```
var windowDad:Window;
var dadWin = new Sprite();
var dadScrollWin = new Sprite();
```

Now, scroll down to the `update()` function, and add this below the `callOnLuas('onUpdatePost', [elapsed]);` line:

```
        @:privateAccess
        var dadFrame = dad._frame;
        
        if (dadFrame == null || dadFrame.frame == null) return; // prevents crashes (i think???)
            
        var rect = new Rectangle(dadFrame.frame.x, dadFrame.frame.y, dadFrame.frame.width, dadFrame.frame.height);
        
        dadScrollWin.scrollRect = rect;
        dadScrollWin.x = (((dadFrame.offset.x) - (dad.offset.x / 2)) * dadScrollWin.scaleX);
        dadScrollWin.y = (((dadFrame.offset.y) - (dad.offset.y / 2)) * dadScrollWin.scaleY);        
```

This sets up the frames for the animations that the dadOpponent plays, so when the window pops up, it plays the correct animations!

Now finally, the function!

```
function popupWindow(customWidth:Int, customHeight:Int, ?customX:Int, ?customName:String) {
        var display = Application.current.window.display.currentMode;
        // PlayState.defaultCamZoom = 0.5;

		if(customName == '' || customName == null){
			customName = 'Opponent.json';
		}

        windowDad = Lib.application.createWindow({
            title: customName,
            width: customWidth,
            height: customHeight,
            borderless: false,
            alwaysOnTop: true

        });
		if(customX == null){
			customX = -10;
		}
        windowDad.x = customX;
	    	windowDad.y = Std.int(display.height / 2);
        windowDad.stage.color = 0xFF010101;
        @:privateAccess
        windowDad.stage.addEventListener("keyDown", FlxG.keys.onKeyDown);
        @:privateAccess
        windowDad.stage.addEventListener("keyUp", FlxG.keys.onKeyUp);
        // Application.current.window.x = Std.int(display.width / 2) - 640;
        // Application.current.window.y = Std.int(display.height / 2);

        // var bg = Paths.image(PUT YOUR IMAGE HERE!!!!).bitmap;
        // var spr = new Sprite();

        var m = new Matrix();

        // spr.graphics.beginBitmapFill(bg, m);
        // spr.graphics.drawRect(0, 0, bg.width, bg.height);
        // spr.graphics.endFill();
        FlxG.mouse.useSystemCursor = true;

        //Application.current.window.resize(640, 480);



        dadWin.graphics.beginBitmapFill(dad.pixels, m);
        dadWin.graphics.drawRect(0, 0, dad.pixels.width, dad.pixels.height);
        dadWin.graphics.endFill();
        dadScrollWin.scrollRect = new Rectangle();
	// windowDad.stage.addChild(spr);
        windowDad.stage.addChild(dadScrollWin);
        dadScrollWin.addChild(dadWin);
        dadScrollWin.scaleX = 0.7;
        dadScrollWin.scaleY = 0.7;
        // dadGroup.visible = false;
        // uncomment the line above if you want it to hide the dad ingame and make it visible via the windoe
        Application.current.window.focus();
	    	FlxG.autoPause = false;
    }
```
    
Use the function, and define the width and height via Int, title, and X! You can also add your own variable to define the y, but for now I made it default to just half of the main window's height.
Like this:

`popupWindow(1280, 720, 'Testing Testing', 500);`

I believe that should be it! 
Thanks for using this awesome code by awesome people :]
JUST PLEASE CREDIT US!!! PLEASE!!!!! ok ok ily <3
