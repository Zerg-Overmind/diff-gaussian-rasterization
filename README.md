# diff-gaussian-rasterization
This repo contains the cuda implementation of variables for calculating Gaussian flow (both forward and backward). While the original repo of 3D Gaussian Splatting is [here](https://github.com/graphdeco-inria/diff-gaussian-rasterization). 

## Install
```bash
git clone --recursive https://github.com/Zerg-Overmind/diff-gaussian-rasterization
pip install ./diff-gaussian-rasterization
```

## Function

```python
rendered_image, radii, rendered_depth, rendered_alpha, proj_means_2D, conic_2D, conic_2D_inv, gs_per_pixel, weight_per_gs_pixel, x_mu = rasterizer(
        means3D = means3D_final,
        means2D = means2D,
        shs = shs,
        colors_precomp = colors_precomp,
        opacities = opacity,
        scales = scales_final,
        rotations = rotations_final,
        cov3D_precomp = cov3D_precomp)
```
Where `proj_means_2D` are the coordinates of Gaussians in image plane, `conic_2D` are the inverse of 2D covariance matrices of Gaussians, `conic_2D_inv` are the 2D covariance matrices of Gaussians, `gs_per_pixel` are indices of top-K Gaussians per pixel, `weight_per_gs_pixel` are weights of top-K Gaussians per pixel, and `x_mu` are x-mu.

Feel free to change `K` from 20 (as in the paper) to another value by modifying [here](https://github.com/Zerg-Overmind/diff-gaussian-rasterization/blob/main/rasterize_points.cu#L64) and [here](https://github.com/Zerg-Overmind/diff-gaussian-rasterization/blob/main/cuda_rasterizer/forward.cu#L386). 

**Acknowledgments**: We thank the following great works [DreamGaussian](https://github.com/dreamgaussian/dreamgaussian), [DreamGaussian4D](https://github.com/jiawei-ren/dreamgaussian4d), [Consistent4D](https://github.com/yanqinJiang/Consistent4D), [RT-4DGS](https://github.com/fudan-zvg/4d-gaussian-splatting), [Dynamic3DGaussians](https://github.com/JonathonLuiten/Dynamic3DGaussians), and [3DGS](https://github.com/graphdeco-inria/diff-gaussian-rasterization) for their codes.
