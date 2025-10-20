Math and shit:
Rotation matrixes

In order to cast rays through all the FOV, we need to be able to calculate the rotation of a vector.
This is the classic rotation Matrixe in two dimension. 
$R=\begin{pmatrix}cos&-sin\cr\sin&cos\end{pmatrix}$

which means with $x$ and $y$ Vector
$x = cos \times x + (-sin) \times y$
$y = sin \times x + cos \times y$ 

To calculate, just add the right column with the left first row, then the right column with the second row
$R=\begin{pmatrix}cos&-sin\cr\sin&cos\end{pmatrix}\begin{pmatrix}x\cr y\end{pmatrix}$

Now we can code our own function to calculate it :
```c
t_vect2	vect2_rot(t_vect2 *a, float angle)
{
	float	cos;
	float	sin;
	t_vect2	result;

	cos = cosf(angle);
	sin = sinf(angle);
	result.x = a->x * cos - a->y * sin;
	result.y = a->x * sin + a->y * cos;
	return (result);
}
```

Now lets use this function to cast rays in all the FOV
We know that we have to cast rays on each pixels of the screen, wich is 1920 pixel wide.
So on an $90\degree$ which is  $\pi / 2$, we will cast 1920 rays with a $\frac{\pi/2}{1920}$ rotation.
So :
```c
	int		length;
	int		r_amount;
	float	fov;
	float	display;
	t_vect2	rotate_dir;
	t_vect2	ray;

	fov = M_PI_2;
	display = fov / 1920.0f;
	r_amount = 1920;
	rotate_dir = vect2_rot(&dir, -fov / 2.0f);
	while(r_amount >= 0)
	{
		length = 80;
		ray.x = mlx->player.x_pos + 20;
		ray.y = mlx->player.y_pos + 20;
		while (length != 0)
		{
			mlx_pixel_put(mlx->mlx, mlx->win, ray.x, ray.y, mlx->color->blue);
			vect2_sum(&ray, &rotate_dir);
			length--;
		}
		mlx->color->blue.g = (mlx->color->blue.g + 1) % 255;
		rotate_dir = vect2_rot(&rotate_dir, display);
		r_amount--;
	}
	return (1);
```

Texture
Pour obtenir la position exacte du mur ou l'on se trouve : 
Selon si le mur touché est vertical ou horizontal :
Position.x\y du mur / par la taille des cellules puis on garde le modulo du flottant de cette operation.

Pour obtenir ce modulo, il faut faire un certains calcul