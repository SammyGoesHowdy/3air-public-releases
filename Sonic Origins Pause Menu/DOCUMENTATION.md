
### Modifying `username.txt` for custom usernames
 * [!] If you have not yet extracted the mod (still in the .zip file), do so and enable the extracted version once you're in game.

1. In the mods folder, open username.txt in your preferred text editor. 
2. Once opened, simply type whatever you want, then save the file.
3. Once in game, set Username Display to Custom (username.txt). 
4. Once you pause the game, your custom username should be displayed, like so:

### Modding stuff :-P

#### Adding character-specific usernames

The "Character" and "Char & Partner" username display options display the names of the main character and/or partner.
 
These options already have built-in automated support for the following character frameworks:
* Extra Character Slots Unlimited (ESU)
* More Independent Slots for Characters (MISC)
* Extra Character Framework (ECF)

But if your framework isn't supported for automation yet, or you just wish to add some fun, you can do as follows:

```cpp
// This code sample is for characters that use the MISC Framework, but should be pretty easy to adapt it for other frameworks.

function string OriginsPause.getCharacterPlayerName(u8 character)
{

	// This is where the check for your character is, be sure to update the variables to match accordingly.
	// And again, please change the check accordingly to match the framework your character uses.
	if (character == CHARACTER_AMY)
	{
		if (OriginsPause.PlayerBarName < 2)
			return "AMY"
	}
	else if (character == CHARACTER_AMY_TAILS)
	{
		if (OriginsPause.PlayerBarName < 2)
			return (OriginsPause.PlayerBarName == 0 ? "AMY" : "AMY & TAILS")
	}

	return base.OriginsPause.getCharacterPlayerName(character)
}
```

#### Adding onto the pre-existing buttons styles

The "Custom (for mods)" button style option allows mods to extend the pre-existing list of button styles.

Your mod should have sprites for A, B, X, and Y, to start the process on adding more options, you can do as follows:

```cpp
function string OriginsPause.getButtonIcon(string button)
{
	if (OriginsPause.ButtonIconStyle == 1)
	{
		// Preferably use the OriginsPause.InputStyle (aka. the "Button Icon" option) for this, though you're free to make it an option in your mod instead, can't stop you. :-P
		// Additionally, you're also free to just remove this part entirely so you only have to focus on one controller type. (generic icons, for example) Just remember to update the stringformat.
		string buttonStyle = (OriginsPause.InputStyle == 0 ? "key" : OriginsPause.InputStyle == 1 ? "ps4" : OriginsPause.InputStyle == 2 ? "ps5" : OriginsPause.InputStyle == 3 ? "xbox" : OriginsPause.InputStyle == 4 ? "switch" : OriginsPause.InputStyle == 5 ? "gens" : "key")

		// This is where your mod options come in to play!
		string iconStyle = (MyCoolMod.ButtonIconStyle == 2 ? "origins" : MyCoolMod.ButtonIconStyle == 3 ? "legacy" : MyCoolMod.ButtonIconStyle == 4 ? "ap" : "origins")

		return stringformat("%s_input_icon_%s_%s",iconStyle,buttonStyle,button)
	}

	return base.OriginsPause.getButtonIcon(button)
}
```