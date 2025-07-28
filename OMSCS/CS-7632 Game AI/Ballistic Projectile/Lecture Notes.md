
## Intro

- We need to consider what forces effect the projectile: gravity, drag, etc.
	- These could also affect the target as well
- Our agent will sometimes need to fire these projectiles at other agents
- It is easy to simulate Newtonian Physics with particle and rigid body dynamics 
- ==The problem is solving for intercepts!==

### Intercept
- Recall Steering Behavior *Pursue*
- An approximate intercept was calculated by estimating how much time it would take for the agent to get in the neighborhood of the target
- Using that time estimate, the target's movement could then be extrapolated assuming a constant velocity
- *Pursue's* intercept time is only estimated because itis going to be updated again the next simulation frame and doesn't need to be precise
- However, with a ballistic projectile, there is only one chance to get the trajectory correct
- Therefore, more computational effort is needed for an accurate trajectory
- Projectiles like grenades or footballs aren't the only game objects that need a precise velocity solved
- Consider a game character like Rhino in Spider-Man
- Rhino might charge Spider-Man but not be able to change direction while charging
- If Spider-Man is running, Rhino's AI needs to calculate a precise intercept
 - Sometimes, it is straightforward to solve an intercept
 - For instance, if the target does not move at all and the projectile is constant velocity (not affected by gravity or drag) then only a relative position vector is needed to get launch direction (scale it by desired speed for full velocity)
 - But what if gravity affects the projectile? Or the target is moving?
 - The more degrees of freedom allowed, the more complicated the system of equations needed solving gets
 - Eventually, the equations can get so complicated that they cannot be directly solved, or become overly complicated or error prone

### Methods
- There are two general methods for solving ballistic projectile launch velocities:
	- **Directly solve** - Formulate a system of equations that represents the problem and directly sole for the unknown variables
	- **Iteratively solve** - Estimate a reasonable solution, then refine parameters until the solution is close enough to the desired outcome.
	- To iteratively solve, the movements of projectile and target must be able to be modeled according to the defined parameters

---

## Static Target with Gravity

### Ballistic Trajectory for Static Target
- Assume 3D positions of projectile and target
- Assume projectile is affected by gravity (but no drag)
- Assume projectile will always be launched at full force
- What is the direction of the velocity to hit the target (if possible)?
- Overview of the relevant variables:
	- $p_t$ - Stationary Target Position
	- $p_{p_0}$ - Initial Projectile Position
	- $u_{p_0}$ - Initial (Launch) Projectile Direction
	- $S_p$ - Initial (Launch) Projectile Speed
	- $v_p$ - Initial (Launch) Projectile Velocity
	- $g_p$ - Gravity Affecting Projectile
	- $t_c$ - Time of collision
- Solve for $u_{p_0}$ because a full speed solution is desired. We only need the direction.
- From Particle Dynamics:
	- $p_t = p_{p_0} + u_{p_0}s_pt_c + \frac{1}{2}g_pt_c^2$
	- This represents three equations (3D):
		- $p_{tx} = p_{p_0x} + u_{p_0x}s_pt_c + \frac{1}{2}g_{px}t_c^2$
		- $p_{ty} = p_{p_0y} + u_{p_0y}s_pt_c + \frac{1}{2}g_{py}t_c^2$
		- $p_{tz} = p_{p_0z} + u_{p_0z}s_pt_c + \frac{1}{2}g_{pz}t_c^2$
	- ![[Pasted image 20250620105155.png]]
	- We need a 4th equations to find the time of collision
		- A fourth can be added since we know that the $u$ vector is a unit vector
		- $\|u_{p0}\| = 1$ 
		- $1 = u_{p0x}^2 + u_{p0y}^2 + u_{p0z}^2$
		- Note that we got rid of Square Root by squaring both sides
- With:
	- $p_t = p_{p0} + u_{p0}s_pt_c + \frac{1}{2}g_pt_c^2$
	- $u_{p0}$ can be isolated
	- $u_{p0} = \frac{p_t-p_{p0}-\frac{1}{2}g_pt_c^2}{s_pt_c}$
	- Let $\Delta = p_t - p_{p0}$ so:
		- $u_{p0} = \frac{\Delta - \frac{1}{2}g_pt_c^2}{s_pt_c}$
- Plug each dimension of $u_{p0} = \frac{\Delta - \frac{1}{2}g_pt_c^2}{s_pt_c}$ into:
- $1=\|u_{p0}\| = u_{p0x}^2 + u_{p0y}^2 + u_{p0z}^2$ giving terms
- $u_{p0x}^2 = \left[\frac{\Delta_x - \frac{1}{2}g_{px}t_c^2}{s_pt_c} \right]^2$
- $$u_{p0x}^2 = \frac{\Delta_x^2 - g_{px}\Delta_xt_c^2+\frac{1}{4}g_{px}^2t_c^4}{s_p^2t_c^2}$$
- Similarly solve for $u_{p0y}^2$ and $u_{p0z}^2$ 
- Note that vectors are losing dimensionality due to the magnitude operation
- 