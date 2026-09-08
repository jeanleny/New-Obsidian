To display the raycasting calculation, we will draw vertical stripes based on the the distance from the player to the next wall collision.

Wall height is calculated with the screen height divided by the cell size.
# $wallheight = \frac{screen height} {cell size}$

Now we have a wall to draw, but it will have a fish eye effect due to way of calculating it.
To correct it, we will multiply the dist by the direction angle divided by the length of the vector director.

# $\frac{dist * dir angle}{vec2dir length}$

Here what it looks like in C
```c
int	get_plan_height(t_mlx_data *mlx, t_vect2 rotate_dir,
		float dist)
{
	int		wall_heigth;
	float	dist_cor;

	dist_cor = dist * (rotate_dir.x * mlx->vec2_dir.x
			+ rotate_dir.y * mlx->vec2_dir.y) / vect2_length(&mlx->vec2_dir);
	wall_heigth = mlx->height * 40 / dist_cor;
	return (wall_heigth);
}
```

From here, we will draw walls from the middle of the screen.
So we'll need to get measure of the ceil and ground.
We can calculate them with the wall height we just got.
# $ceil=$ $\frac{monitor 2}{plan-height 2}$
# $ground=$ $\frac{monitor 2}{plan+height 2}$

in C
```c
int	get_measure(int monitor_h, int plan_h, int *ceil, int *ground)
{
	*ceil = (monitor_h / 2) - plan_h / 2;
	*ground = (monitor_h / 2) + plan_h / 2;
	if (*ceil < 0)
		*ceil = 0;
	if (*ground > monitor_h)
		*ground = monitor_h;
	return (1);
}
```

The check of negative ceil and ground > monitor is to avoid too close camera to the walls.

