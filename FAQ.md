# FAQ

## What is a Dual Gantry printer?

Dual Gantry is a printer layout that enables all the capabilities of a second toolhead (multi-color, multi-material, soluble supports, multi-part), without the complexity and risk of a toolchanger’s attachment interface, or the speed drawbacks of an IDEX.  But in engineering there are always tradeoffs, and the downside is some additional cost, build time, and unknown calibration complexities.

See [Dueling Zero](https://github.com/zruncho3d/DuelingZero) docs for more explanation, including the software side (which is really interesting if you want to have all of the XY space availalable for each extruder's use).

## What's the catch?

A few things...

For some sizes, the carriages stick outside of the frame boundary defined by the extrusions slightly, requiring a panel gap to be covered by something like ZeroPanels (for 1515) or foam tape.  That's not the case for all other Voron gantries, which fit inside the frame.

The specific design doesn't have much attaching to the outer-rail extrusions, so it's not as strong by itself as other designs.  Once in the frame, and braced there with blind screws, it should be fine, though.

The level testing isn't high, either.

And oh yeah, the calibration side can best be described with a question mark.

## Why doesn't this project use the Configurations feature in Fusion 360?

As of October 2023, Configurations is still rolling out slowly to Fusion 360 users.  Since it isn't available to everyone yet, it isn't the default.  

Configurations is made for exactly use cases like this one, though!  Instead of a massively long list of parameters, lacking any organization, and with complex, hard-to-read, hard-to-change nested conditional expressions, Configurations would bring order to the chaos.  And beyond the parameters, you could selectively enable things like the motor spacers on a per-configuration basis, as well as avoid the whole override setup that doubles the number of parameters.  Maybe soon?

Check the ["Configurations Lite" video](https://www.youtube.com/watch?v=n0W37SkbVsI) for more.

## How are Dueling Zero and Dueling X related?

D0 came first.  It was the first open-source, fully-documented, Dual Gantry CoreXY printer design.

DX is a generalization.  At least at the initial release, the bearing positions for DX-Type0 exactly match D0v3... that work bootstrapped this.  

Over time, DX-Type0 is likely to diverge; it has to favor simplicity and ease-of-porting-to-other sizes.

As of the initial release (Oct 2023), there's really no strong reason to go with DX-Type0 over D0v3.  The D0v3 gantry parts have been tested in at least one build, twice ('cuz they're symmetric...) so they're known good.  DX-Type0 _should_ be good, but until you build it, you don't know.

However, D0 includes a complete printer CAD, including integration with a Tri-Zero base and BoxZero frame.  So if you want to make a change (like NEMA17) but keep the 1515 extrusions, you could do that with DX-Customized-Type0 parts inside a D0 frame!