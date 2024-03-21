## Computation of the diffraction pattern with the FFT

The electric field on a screen at a distance $z_0$ from the mask is given by
$E(x) \propto \int_{x'} M(x')\exp\left(\frac{-2i\pi x' x}{\lambda z'}\right)dx'$
with

$M(x')=E_i(x')A(x')\exp\left(\frac{i\pi x'^2}{\lambda z'}\right)$

Discretization:

$E(x_k) \propto \sum_{j=0}^{N-1}M(x_j')\exp\left(\frac{-2i\pi x_j'x_k}{\lambda z'}\right)$

Posing

$x_j'=j\Delta x'$ and $x_k=k\Delta x$

we have

$E(x_k) \propto \sum_{j=0}^{N-1}M(x_j')\exp\left(\frac{-2i\pi j\Delta x'k\Delta x}{\lambda z'}\right)$

The FFT computes

$E_k = \frac{1}{N} \sum_{j=0}^{N-1}M_j\exp\left(\frac{-2i\pi jk}{N}\right)$

Identification of the terms gives

$\frac{jk}{N} = \frac{j\Delta x_k'\Delta x}{\lambda z'}$

whence

$\Delta x=\frac{\lambda z'}{N\Delta x'}$

### At infinity: Fraunhofer diffraction
$M(x^{j'})\xrightarrow[z' \to \infty]{} E_i(x^{j'})A(x^{j'})$

The diffraction is computed by the FFT at discrete angles $\alpha^k$ given by
$\alpha^k=k\frac{\Delta x}{z'}=k\frac{\lambda}{N\Delta x'}=k\Delta\alpha$

### Choice of sampling

Since the grid pitch is a multiple of the thickness $T$ of the rods, we choose $\Delta_x$ to be a sub-multiple of the width of the rods, so that each cell is sampled identically:
$\Delta x'=\frac{T}{q}$ with $q \in \mathbb{N}$

This also forces $\Delta \alpha$ to be set, while we want to compute $E_k$ at angles corresponding to the plate scale $P$ (expressed in radians) or its submultiples:

$\Delta\alpha = \frac{P}{m}$ with $m \in \mathbb{N}$
Both conditions can't be jointly fulfilled strictly, for:
$\Delta \alpha=\frac{\lambda}{N\Delta x'}=\frac{P}{m}\implies m=\frac{NPT}{q\lambda}\notin \mathbb{N}$
since $N$ is an integer. Conversely, the $N$ that gives the closest approximation to the desired $m$ is
$N=\frac{mq\lambda}{PT}$
rounded to the nearest integer. Rounding implies that in practice is not an integer. The diffraction is thus computed at angles that are not submultiples of the plate scale. However, the relative error on $m$ is at most $1 / 2N$.

The physical width of the map that represents the diffracting aperture is given by
$N\Delta x'=m\frac{\lambda}{P}$
which means that $m$ has to be sufficiently large so that $N\Delta x_0$ is larger than the aperture.
The width of the diffraction map is given by
$N\Delta\alpha=q\frac{\lambda}{T}$
The value of $q_{max}$ required to compute the PSF over the full FOV $n\Delta\alpha$ ($n$ being the width of the image in pixels) is given by.
$q_{max}=n\frac{\Delta\alpha T}{\lambda}$

### Polychromatic PSF

The diffraction pattern is a function of the incident wavelength. The solar radiation being polychromatic, the total PSF is the sum of the PSFs at all wavelengths. We want the angular sampling $\Delta\alpha$ and the oversampling factor $m$ to remain the same at all wavelengths. The integer $N$ that gives the best approximation to the desired integer $m$ increases with $\lambda$, which slows down the computations. However, since we do not need to compute at angles larger than $N_0\Delta\alpha$, it is possible to decrease $q$ to the largest value that still ensures $N\geq N_0$. This condition is also sufficient to ensure that the coverage of the entrance aperture is at least that with the shortest wavelength. Indeed:

$\frac{N\Delta x'}{N_0\Delta x_0'}=\frac{N}{N_0}\frac{q_0}{q}$

And thus $N\Delta x' \geq N_0\Delta x_0'$ since $N\geq N_0$ and $q_0 \geq q$

