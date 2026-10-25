# Pill battery with percentage inside (levels 0 to 100)

res/drawable/
- ic_battery_pill_0.xml ... ic_battery_pill_100.xml : one vector per level
- ic_battery_pill_level.xml : LevelListDrawable, set level = battery percent

Usage (Kotlin):

    val d = ContextCompat.getDrawable(ctx, R.drawable.ic_battery_pill_level)!!.mutate()
    d.level = percent            // 0..100
    d.setTint(statusBarIconColor)

How it works
- Track is the icon colour at 60% alpha, fill is the icon colour at 100%.
- The fill ends in a straight vertical edge, clipped to the pill.
- The percentage is a cut-out (see-through), so a single tint works on light and dark
  status bars. The digit colour is whatever sits behind the icon.
- Intrinsic size is 25.5dp x 15dp (ratio 1.7). Change width/height in each file, or set
  bounds in code. The viewport is 34 x 20 with no padding.
- Needs API 24+ (evenOdd fill type).
- Low-battery red / charging colours are not baked in; apply them with setTint or ask for
  coloured variants.

Digits
- The percentage uses the supplied OneGitSans font (Google Sans Flex, opsz 12, wdth 100,
  GRAD 50), converted to plain vector outlines, so no font is needed at runtime.
