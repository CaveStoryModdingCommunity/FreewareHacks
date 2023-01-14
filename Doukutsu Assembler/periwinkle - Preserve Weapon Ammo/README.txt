This hack preserves weapon stats (level, exp, ammo) when a weapon is removed
(via <AM- or <TAM) and later re-added (via <AM+ or <TAM).
This data is stored in the space used by the map flags (<MP+ etc.), but if your
mod needs map flags for some reason (or if it uses another hack that also uses
that space) then you can change where the data gets saved by editing the
addresses in Sources/defines.txt and then regenerating the patches using DouA.

Also, this hack completely rewrites the AddArmsData, SubArmsData, and TradeArms
functions (the author got lazy and used a compiler; sorry ASM gurus), and hence
will be incompatible with any hacks that modify the behavior of these functions
(can't think of any off the top of my head).


***** IMPORTANT NOTE: Changes to vanilla behavior *****

The ammo parameter of <AM+ and <TAM behaves slightly differently than vanilla
in this hack.

> For <AM+xxxx:yyyy:
If you currently have weapon xxxx, adds yyyy ammo to it (same as vanilla)
If you do NOT have weapon xxxx, gives you weapon xxxx with ammo as follows:
OLD/VANILLA BEHAVIOR: the new weapon will have yyyy ammo
NEW BEHAVIOR: the new weapon will have ammo equal to
        (ammo from the previous time the player had weapon xxxx) + yyyy.
(If this is the first time obtaining weapon xxxx, then it will have yyyy ammo,
as expected.)

> For <TAMxxxx:yyyy:zzzz:
OLD/VANILLA BEHAVIOR: the new weapon will have ammo equal to
    (current ammo of weapon xxxx) + zzzz
NEW BEHAVIOR: the new weapon will have ammo equal to
    (ammo from the previous time the player had weapon yyyy) + zzzz.
You can get the old (vanilla) behavior by making the first digit of the
ammo count 9, e.g. <TAM0001:0002:9015 sets the new weapon 2's ammo
equal to weapon 1's ammo + 15, whereas <TAM0001:0002:0015 woulld set it
to weapon 2's previous ammo + 15.


If needed, the saved weapon stats values can be edited directly via OOB flags.
You'll probably have to ask for help on how to do this, but just for
documentation purposes, here's the format of the saved weapon data:
Start (weapon 0): address 49E5B8 (flag 16576 = "@576" in TSC)
8 bits - weapon level (minus 1)
8 bits - weapon exp
16 bits - weapon max ammo
16 bits - weapon current ammo
(then repeat for weapons 1-13)
