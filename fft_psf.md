## Computation of the diffraction pattern with the FFT

The electric field on a screen at a distance $z_0$ from the mask is given by
$E(x) \propto \int_{x'} M(x')\exp\left(\frac{-2i\pi x' x}{\lambda z'}\right)dx'$
with

$M(x')=E_i(x')A(x')\exp\left(\frac{i\pi x'^2}{\lambda z'}\right)$

Discretization:

$E(x^k) \propto \sum_{j=0}^{N-1}M(x_j')\exp\left(\frac{-2i\pi x_j'x_k}{\lambda z'}\right)$

Posing

$x_j'=j\Delta x'$ and $x^k=k\Delta x$

we have

$E(x_k) \propto \sum_{j=0}^{N-1}M(x_j')\exp\left(\frac{-2i\pi j\Delta x_k'\Delta x}{\lambda z'}\right)$

The FFT computes

$E_k = \frac{1}{N} \sum_{j=0}^{N-1}M_j\exp\left(\frac{-2i\pi jk}{N}\right)$

Identification of the terms gives

$\frac{jk}{N} = \frac{j\Delta x_k'\Delta x}{\lambda z'}$

whence

$\Delta x=\frac{\lambda z'}{N\Delta x'}$

