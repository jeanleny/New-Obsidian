The DDA is an algorithm that iterates over each squares of a grid map with rays.

It will get us the position where the ray strikes a wall and his the distance from the player to the wall.
 
```c
 float	get_ray_distance(t_mlx_data *mlx, t_vect2 dir, t_ray_prop *ray)
{
	int				step_x;
	int				step_y;
	float			complete_length;

	step_x = 0;
	step_y = 0;
	complete_length = 0;
	set_ray_pos(mlx, &ray->curr_pos, &ray->curr_map);
	while (wall_hit(mlx, ray->curr_pos.x / 40,
			ray->curr_pos.y / 40, dir) == FALSE && complete_length < 800)
	{
		set_ray_prop(ray, dir, step_x, step_y);
		set_ray_axis(ray, &complete_length, &step_x, &step_y);
	}
	return (complete_length);
}
```

This loop will set properties and axis to each rays until it strikes a wall.
Each loop is each square that the ray pass through.

![[Pasted image 20251021102528.png]]

This drawing represent how the rays priorize a side.

To get the next side we're using this function
```c
t_vect2	get_next_side(t_vect2 dir, t_coord curr_map, int step_x, int step_y)
{
	t_vect2	next_side;

	if (dir.x < 0)
		next_side.x = (curr_map.x - step_x) * 40;
	else
		next_side.x = (curr_map.x + step_x + 1) * 40;
	if (dir.y < 0)
		next_side.y = (curr_map.y - step_y) * 40;
	else
		next_side.y = (curr_map.y + step_y + 1) * 40;
	return (next_side);
}
```

In this function, we're using steps to go to each square of the grid wich will increments at each loop.

Then we calculate the distance of the player to the next side on x and y position
with projection function.

```c
float	vect_projection(float player_pos, int next_side)
{
	float	result;

	if (next_side < 0)
		result = (next_side - player_pos) + 1;
	else
		result = next_side - player_pos;
	return (result);
}

t_vect2	get_proj_x(float pos, float next_side, float dir1, float dir2)
{
	t_vect2	proj;

	proj.x = vect_projection(pos, next_side);
	proj.y = (proj.x * dir1) / dir2;
	return (proj);
}
```

Note that we need a `get_proj_x` and a `get_proj_y` function for each side.

![[Pasted image 20251021103656.png]]
On this image, we replaced the x and y axis with A and B.
The B projection is just our player position minus the next side.
The A projection is determined by our director vector.

Now that we have these measurement, we can apply pythagoras theorem.
```c
float	pythagoras(float a, float b)
{
	float	result;

	result = sqrtf(a * a + b * b);
	return (result);
}
```

Now we can check what distance to the next side is shorter and keep this one.
Note that you keep the the new distance endpoint as the new player position.
At the end of the loop we would have an accumulated distance of each square the we can pass to the [[Rendering]].