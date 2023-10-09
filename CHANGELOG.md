### Changelog / Updates

* 2023-10-09; v76
    * Finish test piece to ensure unknown values are reasonable.  Has extrusion tab slots in 3 orientation, holes that match the ab extrusion spacing, clearance holes, formed thread holes, and bearing screw clearance holes.
    * Fix under-constraint error for X location of AB lower/upper locking tabs
    * Add instructions for testing the test part
    * Finish all documentation and edit for clarity and conciseness (I know, I know…)
    * Document relationship between Dueling Zero and Dueling X
    * Push to GitHub as private and wait to flip the bit to make this thing public!!!
* 2023-10-08; v74
    * Type 2: Tweak params to get 10mm-aligned AB extrusion length (ab_extrusion_width_computed)
    * Add motor_spacer_opening_r to easily enable the motor plate to fit a bearing
    * Clear away all obsolete and unused parameters
    * Tag all parameters that require tuning
    * Definite minimal set of favorite params
    * Make progress on test part to ensure correct values for tunable params
* 2023-10-07 v71
    * Fix model break when either extrusion_length_x parameter is changed, or when type is cycled
      * Remove all top-edge fillets, to simplify debug
      * Remove an inadvertently split line in the base sketch, then fix all broken downstream references
      * Fix a computation failure by switching to a parallel constraint instead of a tangent one
      * … and it seems more stable now
    * Docs mostly converted to Markdown for Github usage, with exception of pre-release checks (which are getting defined)
* 2023-10-02 v70
    * Fix thin-wall error near Type 1 tensioner heatset hole
    * Add back extrusion hole to the side
    * Label all sketches, work planes, features, groups, and bodies appropriately
    * Components for everything
    * Ensure easy-starts with hole chamfers
    * Ensure feasible screw sizes: adjust XY joint top height, XY joint lower thickness, and AB bearing hole depths
    * Create BOM for Type0 and Type1 XYs and ABs
* 2023-10-01 v62
    * Generalize AB-connector extrusion from main frame extrusion (narrower if you want); update lots of dimensions to match
    * Add inner corner fillet at the AB elbow
    * Add extrusion slot tabs to ABs
    * Fillet and chamfer ABs
    * Add top-edge chamfers
    * Angle leading edges of extrusion slot tabs
    * Add mirrored side of XYs, with flipped filling
    * Fillet XY elbows
    * Smoothen wire-clearance cutaways on XYs
    * Add extrusion slot tabs to XYs
    * Fillet and chamfer XYs
    * Mirror ABs and belts and join belt bodies
* 2023-09-30: v52
    * Fix thin-wall error in AB lower tab
    * Fix rear tensioner heatset location; was too far back
    * Tweaked key params for Type 1 and Type 2 setups for carriage-screw access and to fix belt-bearing interferences: `ab_exposed_bearing_y_spacing, ab_innermost_bearing_rear_y_offset_derived`
    * Fix belt interference with ABs
    * Fix unmatched AB extrusion tip
    * Fix front AB clearance
    * Fix scaling of rail cutout in AB near rear bearing hole
    * Fix XY and AB heights so that all outer carriage screws can be inserted in-place
    * Fix XY top thickness to scale
    * Close rear bearing hole on Type 2
    * Make XY allen clearance holes parametric and larger with Type 1 & 2
    * Improve X travel to max possible for Type 1 and Type 2
    * Add cutouts for carriage clearance, scaled to type
    * Add bridged counterbore for front AB bearing screws to clear + adjust for each type
    * Make motor spacer thickness parametric + adjust for each type to fit known screws
* 2023-09-25: v42
    * Add filling in the XY joints
    * Fix annoying-af nondeterminism that was breaking the base sketch when 0-2-0 switching
    * Fix overlap on larger types with XY front hitting ABs
    * Add belts
* 2023-09-24: v35
    * Reduce cutaways by tensioners, heavily
    * Reduce plate overlap with extrusions and make parametric
    * Using measurements taken from Trident, reduce width with denser screws: 9mm to edge, 16mm between, vs 10/20mm previously. Now the 2020 version fits on a V0 plate (117mm wide)
    * Fix thin wall in rear, near motor screw
    * Expand tensioner ramp and made it parametric: ab_tensioner_front_ramp_min_thickness
    * Add belt travel; now 8mm for 2020; less than Trident’s 10mm at the moment, but better.
    * Tensioner heatset setback matches screw travel now
    * Temporarily remove side extrusion screw holes; will likely be replaced with two screws in the future, but larger changes
    * Define critical param to align carriage: xy_joint_carriage_offset_from_moving_extrusion_derived
    * Create XY upper and lower bases, then validate for 3 sizes; still needs the middle bits added, plus cutouts for endstop clearance
* 2023-09-23: at v21
    * Define and use belt_rear_clearance to pull bearings near verticals and reduce overall width
    * Define width of ABs based on geometry
    * Added tensioner ramp and matching tensioner; redid all related geometry to ensure bearing clearance and sufficient space forl tensioner travel.
    * Added side extrusion-grab hole
    * Rename motor_slot_length → tensioner_travel
* 2023-09-22: v15
    * Make frame extrusion type an explicit param
    * Add type 2 and corresponding values: Trident Maximum Duelingus: 3030+2020, NEMA23, F695, all MGN12
    * Added constraints to make type 2 look right
    * Scale width of motor pulley access hole with extrusion size
    * Marked all most-likely-to-change parameters as favorites
* 2023-09-XX: Time to rebuild from scratch
    * Rebuilding is painful, but sometimes it’s the only way to make progress.  The D0 v3 CAD was freshly recreated from the v1 CAD, but with compute failures in the base sketch, it’s really hard to debug what parameters are colliding, as well as even navigate within the model.  If you want to have multiple sizes in a model, you can slowly refactor it there, or you can start from the beginning, leveraging what you know, and testing continually to make sure all sizes don’t have issues.
    * Decision taken to start over, and leverage conditional parameters from the beginning, as well as multiple, more hierarchical sketches.  This means:
        * Define at least two configurations before building the model - “types” - V0 + Trident sizes
        * Define many parameter values (_derived) ones based on the type, using if statements in the parameters dialog
        * Aggressively test all new features against all types to ensure that things are scaling
        * Generalize parameters wherever possible
* 2023-09-16:
    * Dueling Zero stream on DoomCube live goes well!  Peaks around 80 viewers.  
    * Interest seems more for 2020 than 1515, which makes a lot of sense. Larger builds are more practical and kits have dropped the prices for Tridents and V2s lately.
    * Time to make this happen, finally.  At this time, Dueling X is really more an idea than an implementation; the D0 v3 CAD has lots of parameters, but alternate sizes were not tested.