# Transparent-and-MultiWindow-FNF

Yeah! This is the code for transparent windows and mutliple linked windows for FNF code. This can also be used for other stuff, but this is a template for FNF code.

THIS ISN'T IN LUA!! ITS HARDCODED (in psych engine) !!!!!!!!!!!!!

So, first off, Transparent windows! 

So, first off you are going to want to make a bg sprite like this:

```var bg:FlxSprite = new FlxSprite().makeGraphic(FlxG.width, FlxG.height, FlxColor.fromRGB(1, 1, 1));
if (defaultCamZoom < 1)
{
  bg.scale.scale(1 / defaultCamZoom);
}
bg.scrollFactor.set();
add(bg);```

Then, afterwards, put the line `FlxTransWindow.getWindowTransparent();` directly below it.
This will make the sprite of `bg`, and everything below it, transparent!
You can add sprites above it to hide it, and toggle the visibility to reveal the transparent window.

WARNING: ANY PIXELS WITH AN ALPHA BELOW ONE WILL HAVE BLACK BELOW IT, LIKE THIS
![] (https://albumizr.com/a/ooQVkw)
