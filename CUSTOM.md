# Custom configurations

Say, you want to make a variant, like 1515 + NEMA17… will it work?  You may need to tweak some positions to ensure clearances.  Ensure the conditions below to make sure your Dueling X build can actually be assembled, uses screw sizes that exist, and can actually move.

Think of it as a giant puzzle that you have to solve.

Or… **get** to solve.  I prefer the (more thankful) latter interpretation.

First, set the type value to the closest one to your target, to minimize the number of parameters to override.

To see a model in a non-default type, open the f3z, go to the parameters screen, and change the type value from the number 0 to 1 or 2.  Assuming your Fusion install is set to recompute parameters automatically (the default) the model will then adjust to the new size.

## What can I customize?

All of the stuff that has a corresponding `_derived` expression is meant to be customized; the `_derived` expression is effectively a default, for the `type`.

To set a value, go to Parameters and give it a value you want, vs the `_derived` version.

Sample parameters that you may want to override (customize):

* Extrusion widths: main (outer rails) + moving + "AB connector"; each can be different!
* Width (X dimension)
* Length (Y dimension)
* Belt width
* Rail/Carriage sizes
* Bearing sizes: example - 2020 with F623 bearings for more travel
* Motor type/size
* Plate thicknesses (against the motor, and on top of the ABs)
* Center diameter of motor spacer (to enable double-supported motors, by adding another bearing on the end)

This list is not exhaustive; there are also other parameters that decide where the bearings go, from which all other part shapes are derived.  For example:
* `xy_joint_carriage_offset_from_moving_extrusion_rear` moves the carriage position up or down on the model.

## Examples of customizations

### Double-supported motors

Easy!  Change `motor_spacer_opening_r` to a new value.

### Wider outer carriages

Say, not so hypothetically, `shadow_steve` seeks wider outer carriages (the rails with two carriages).  

Steps: replace the default `_derived` value: set `inner_carriage_type` → 9
Then follow steps below to see what stuff to check and what params to adjust At least these two are needed:
* `ab_joint_shoulder_depth` → 12mm
* `xy_joint_carriage_offset_from_moving_extrusion` → 3.4mm
If all the items below are OK, plus a full section analysis check out, you can move to STLs!

# How do I navigate the model?

Start with the base sketch!  Everything derives from this, like the belt paths, bearing positions, XY joint positions, and resulting travel.  Every single dimension here is critical.

Anything which is not strictly dependent on the bearing and extrusion positions gets its own sketch, which should use an absolute minimum of references to base sketch geometry, to minimize model fragility.  So often, you'll need to find the right sketch after the base one to understand a parameter and change it.  All sketches are labeled, to make this search process a little faster.

Use the timeline as much as you can to navigate the model effectively.  If you're just changing the ABs, go there first, and then switch between types with less recomputation delay.  Stepping through each group of features makes it much faster to find what you want.

# Pre-printing Checks

More details to be added here... this section notes checks to do before generating STLs (whether you for your custom build, or Zruncho at release time)

You want to ensure 3 things:
* Prints can succeed
* Printed parts are sized to match real parts
* Gantry can actually be assembled

These sound obvious... but it's possible to get them all wrong.

### Condition: Belt path is possible

A belt can't pass through a bearing.  You may have to tweak some values so that this is the case!

### Condition: Generally good parts for printing

No overly thin walls, no unsupported overhangs... typically a section analysis through the whole model will reveal these.  

Sometimes area selections get silently lost when parameters change, and the only way to catch those is to scan the whole model visually.

### Condition: Access to tighten outer carriage screws

… or at least with an amount of tilt so small that you can still get the driver in.

Param to adjust: `xy_joint_carriage_offset_from_moving_extrusion`

Potential values in `xy_joint_carriage_offset_from_moving_extrusion_derived`

Process: adjust the timeline position to after the XY joints are created.  Click on the belts to highlight them in blue.  Look for a gap through which an allen driver can be inserted, without impacting the bearing flange.  Look at the `Carriage Alignment` sketch, which decides the positioning of carriage bits.

With Type 0, there’s no way around a tight fit; MGN7H carriages have a long-carriage-direction screw spacing that nearly matches the flange OD of F623 bearings.  So one of the carriage-screw holes must be aligned between the two moving bearings, and then you hope that the bearing on the other side has clearance.  The location is manually aligned by moving the carriage holes relative to the bearings on XY joints.  

### Condition: Sufficiently thick walls at rear edge of XY

Param to adjust: `ab_joint_shoulder_depth`

Solutions can include increasing this value to enable a complete counterbore for the rearmost XY-joint carriage screw OR reducing it to have a partially-overlapped hole (like the 1515 version).

### Condition: Sufficient belt clearance between frontmost two outer AB bearing stacks

Param to adjust: `ab_exposed_bearing_y_spacing`

Param to adjust: `ab_innermost_bearing_rear_y_offset_derived`

The smaller this is, the greater the potential moving-extrusion travel.

### Condition: viable screw lengths exist to match all holes

Especially if changing AB part thicknesses (say, due to modifying belt widths), you have to ensure that all screws have enough length to fully form threads.  

**Screws for bearings**: check them all; these are the easier ones.  You need a few mm of screw engagement in the formed threads.

**Front AB bearings**: adjust `ab_front_bearing_counterbore_dia` so front screw head is contained, yet, screw does not stick out, and also has a little travel to fully compress the counterbore there.  M5 example: 9.5mm dia, 2.75mm head thickness.

**Motor screws**: The motor spacer part provides a lower-plastic way to get the height right for motor screw, without needing to adjust everything else to be thicker.

# Release Process

For releasing the whole model, the checks are broader that those of a single variant.

### Condition: Parameters can be varied (DX releases only)

Mostly: change the type in both directions (0 - 1 - 2 - 1 - 0) and ensure no yellow warnings or red errors appear in the timeline.

Then vary all the favorited parameters and ensure that huge values don't create issues either.

Both of these can break without you noticing, and sometimes parameters can compute nondeterministically, where it appears to randomly break.  When this happens, you may need to change the kinds of constraints that are used in base sketches or break complex features into multiple stages or sketches.  It feels like a dark art, until you internalize what's really going wrong.
