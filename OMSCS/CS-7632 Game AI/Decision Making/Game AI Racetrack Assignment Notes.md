
---
# Tips 
## General

1. Make regular backups so you can revert to a working version if you make a breaking change
2. Use fewer fuzzy states as possible to start with (e.g. left, straight, right, or brake, coast, accelerate). You can always add more later (e.g. hard left, slight left, etc.)
3. Do not use **Boolean** logic to start with (AND, OR). It is fine to overlap rules in terms of output effects as long as they are not completely mutually exclusive since defuzzification blends.
4. You might tackle steering first and wait on throttle. You can do this by using `HardCodeThrottle(v)` command. You **must** still implement variable/fuzzy throttle control as your final, submitted solution though!
5. You can also comment out subsets of the rules that involve a particular strategy. For instance, you might have steering rules that evaluate lane position. You can test those in isolation. Then test rules for relative road direction in isolation. Them combine them, etc.
6. The `pathTracker` and `pathTracker.pathCreator` both provide information about the road that will be useful for defining crisp value observations (inputs). Be sure to check out the descriptions in the assignment readme and discussions in Piazza posts.
7. Make sure you have overlap in your *DoM* functions for Fuzzy input variable states. Without overlap, there will be no interpolation between values.
8. You can check out `FL_3DBall` as well as the script `FLBall3DAgent.cs` to get a live demonstration of Fuzzy Logic decision making for steering a vehicle.
9. Be ware of using a shoulder function configured to have a large plateau on the extreme left/right sides of your crisp **output** value range. Plateaus are problematic because of the way defuzzification works with the provided API which is based on Buckland's Representative Value approach (*Mean of Maxima*). Instead, think about which Representative Value you want for each fuzzy state.
10. Say you want to have a fuzzy state for `TURN_LEFT`. You might think to define your function to be a *DoM* of $1.0$ for crisp values, $-1$ to $-0.5$ (e.g. a plateau) and then taper down to $0.0$ *DoM* at $0.0$ crisp value. However, what ends up happening is that you will have a representative value of the average crisp value of the plateau so you get $-(-1.0 + -0.5) / 2 = -0.75$. This means *that* during defuzzification it is impossible to get a full $-1.0$ turn rate. You will probably want to shrink the plateau so that the representative value is $-1.0$. 
	1. Example of a shoulder without a plateau:
	2.
```C#
var left = new ShoulderMembershipFunction(-1f, new Coords(-1f, 1f), new Coords(0f, 0f), 1f) // plateau on left shrunk to a point 
```
## Debugging

1. You can visualize vectors and positions (probably for crisp input values) with `Debug.DrawLine()`, `Debug.DrawRay()`,  override `OnDrawGizmo()` and draw a gizmo shape like a sphere at some position, or just add some Game Objects to the scene with appropriate scripts for updating position. By default, these only show up in the Scene view. But you can also enable them in the Game view as well. 

## Advanced Racing Strategy

1. The truck has all-wheel drive. The driving dynamics may be unexpected if you assume rear wheel drive.
2. If you truck is going really fast while turning it will likely either roll over or spin out. Your agent might reactively correct this with counter steer (opposite lock). You might measure how much the truck is leaning or if velocity is not in the direction the truck is facing (e.g. sliding).
3. If you real want to push it:
	1. You can determine turn radius (assuming your truck is not sliding) with: `turnRadius = wheelbase / Tan(currentTurnAngleInRadians)`. 
	2. The trucks' wheelbase is $2.16$ meters. Use `AIVehicle.Steering` to get steering angle in degrees.
	3. The center of the turn radius is located perpendicular to the forward direction of the truck, either left or right depending on direction of turn. Once you identify the center of the turn radius you can then find a future point along the turn arc pretty easily: `arcLength = thetaInRadians * radius`.
	4. ==This technique can be more effective than linear extrapolation of the trucks' movement!==

## Defining Membership Functions

All the DoM functions are piecewise linear functions defined by points. 

Example: `public ShoulderMembershipFunction(float minX, Coords p0, Coords p1, float maxX)`

The arguments to the shoulder function constructor are as above. You can think of all four as endpoints in the line segments that make up the piecewise linear function.

`minX` and `maxX` are $x$ values. The $y$ values are implied to be whatever the $y$ value is of the other endpoints that they connect to. `p0` and `p1` have both $x$ and $y$ values. The order that `p0` and `p1` are defined does not matter. The constructor sorts them so that whichever has a smaller $x$ is listed first.

You can think of the four endpoints of the piecewise linear function as: 

`(minX, P0.Y), (P0.X, P0.Y), (P1.X, P1.Y), (maxX, P1.Y)`

`P0` has the smaller $x$ attribute and `P1` has the larger. Any $x$ to the left of `minX` is considered to be on a horizontal line at height `P0.Y`. Any $x$ to the right of `maxX` is considered to be on a horizontal line at height `P1.Y`. Between `P0` and `P1` is a point at $x$ which will be on the line formed between those two points.

<figure style="text-align: center;">
  <img src="Pasted image 20250713181549.png" alt="Description" width="400">
  <figcaption style="font-style: italic">Figure 1: Should function diagram.</figcaption>
</figure>

---

When to break
- approaching a barrier
- approaching a turn
- approaching a speed limit?

When to accelerate 
- coming out of a turn
- At the start 