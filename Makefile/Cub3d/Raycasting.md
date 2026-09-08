Raycasting is a rendering technique to create a fake 3D perspective in a 2D map.
So we cast rays from the player position that simulate a "camera".

This camera will cast rays until it find a wall or the max rendering distance.
The rays will go through the 2D map performing a [[DDA]] algorithm.

Each rays are shot as much as the screen width resolution.
In our case, there will be 1920 rays shot for the 1920 pixel screen resolution.

In C
```c
int	ft_rays(t_mlx_data *mlx, t_vect2 dir)
{
	int		r_amount;
	t_vect2	rotate_dir;

	r_amount = 0;
	rotate_dir = vect2_rot(&dir, -mlx->fov / 2.0f);
	set_img(mlx);
	while (r_amount <= 1920)
	{
		raycast(mlx, &rotate_dir, r_amount);
		r_amount += 2;
	}
	mlx_put_image_to_window(mlx->mlx, mlx->win, mlx->img->room, 0, 0);
	return (1);
}
```

The first ray will begin at the start of our FOV (PI / 2 in our case) using our [[Rotation]] function.
The set_img is a function that display the ceiling and the floor of the maze at each frame.
Notice that the r_amount is increased by 2, at the beginning, the increments were one by one, but to optimize, we decide to calculate the rendering on 2 stripes per calculation.
It affect the rendering on high resolution images, and only on longer distance.
