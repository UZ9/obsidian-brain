#physics

##### Nothing is moving, but different angle
1. Find angle between current ship and enemy ship

Newton's Second Law

$$
\begin{gathered}
\text{Newton's First Law:} \\\\
\text{An object in motion will stay in motion unless }\\\\
\text{a non-zero force is applied to it}
\end{gathered}
$$
$$
\begin{gathered}
\text{Newton's Second Law:}\\\\
\vec{F_{net}} = \frac{\Delta p}{\Delta t}\\\\
\text{Resulting Kinematics Equations:}\\\\
v_f = v_i + \frac{\vec{F}_{net}}{m}\Delta t\\\\
r_f=r_i+v_{avg}\Delta t
\end{gathered}
$$


$$
\begin{gathered}

\text{1. Find the angle between the ship's current position and the enemy's ship:}
\\\\
\tan{\theta_{target}} = \frac{y}{x}
\\\\
\theta_{target}=\arctan{\frac{y}{x}}
\\\\
\text{2. Define error as difference between actual and target: }
\\\\
E(T) = \theta_{target} - \theta_{actual}
\\\\
\text{3. Set angular acceleration based on error:}
\\\\
\alpha(t) = clamp(E(T), \alpha_{min}, \alpha_{max}) 
\\\\
\text{4. Calculate corresponding angular velocity}:
\\\\
\omega = \omega_0 + \alpha t \\
\omega = \omega_0 + (clamp(E(T), \alpha_{min}, \alpha_{max}))
\end{gathered}

$$


```rust
// Check if absolute error is less than threshold
if (target_angle.abs() < 0.05 && angular_velocity < 10.0) {
	// Fire weapon, as we're facing the correct angle
	fire(0);
}
```


##### Our ship isn't moving, but the enemy is
Notes:
- Non-constant acceleration
- Non-constant velocity

$$
\begin{gathered}
\text{Bullet Speed = $V_b$}\\\\
\text{1. Calculate predicted enemy position after $\Delta t$ seconds:}
\\\\
\text{Amount of time to }\\
t = \frac{\left|\vec{r_i}\right|}{V_b}
\\\\
a = \frac{\Delta v}{\Delta t} 
\\\\
\vec{r_f} = \vec{r_i} + \vec{v}t + \frac{1}{2}at^2
\\\\
\text{$r_f$ represents the position the ship will be in by the time the bullets reach.}
\\\\
\text{2. With the new ship position, predict position if the ship shot at $r_f$ instead:}
\\\\
t = \frac{\left|\vec{r_f}\right|}{V_b}
\\\\

\end{gathered}
$$