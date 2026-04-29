# Lab Log

## 2026-04-11

### What is PSF?

PSF stands for **Point Spread Function** — it describes how a perfect point source (like a distant star) appears after passing through the atmosphere and telescope optics.

A star should be a single point of light, but it gets **blurred** into a blob due to:
- **Atmospheric turbulence** (seeing) — the biggest effect for ground-based telescopes
- **Optical diffraction** and aberrations in the telescope
- **Detector effects** (charge diffusion, brighter-fatter)

**Why it matters for shape measurement:** The PSF distorts galaxy shapes. A round galaxy will look elongated if the PSF is elongated. To get the *true* galaxy shape, you have to model the PSF and correct for it. Checking that the PSF model is good is essential before trusting shear measurements.

In short: PSF = the "blur kernel" of the telescope. Know the blur, undo the blur, get the real galaxy shape.

---

### What is a trace of moments?

In shape measurement, **moments** are weighted integrals over a galaxy's light distribution:

$$Q_{ij} = \frac{\int I(\mathbf{x}) \, x_i \, x_j \, w(\mathbf{x}) \, d^2x}{\int I(\mathbf{x}) \, w(\mathbf{x}) \, d^2x}$$

This gives a 2x2 **moments matrix**:

$$Q = \begin{pmatrix} Q_{xx} & Q_{xy} \\ Q_{xy} & Q_{yy} \end{pmatrix}$$

- **Q_xx** — how spread out the light is in the x-direction
- **Q_yy** — how spread out in the y-direction
- **Q_xy** — how much the light is tilted/correlated between x and y

The **trace** is:

$$\text{Tr}(Q) = Q_{xx} + Q_{yy}$$

This gives the **overall size** of the object — the total spread regardless of direction. It doesn't care about shape or orientation, just how big something is.

Key insight:
- **Ellipticity** (shape) comes from the *differences* between Q_xx and Q_yy and from Q_xy
- **Size** comes from the *trace* (sum), e.g. $r^2 = Q_{xx} + Q_{yy}$

Both matter for weak lensing — the PSF affects both the size and shape of galaxies, and you need to correct for both.

---

## 2026-04-16

### What are e1 and e2?

**e1** and **e2** are the two components of ellipticity, defined from the second moments matrix Q:

$$e_1 = \frac{Q_{xx} - Q_{yy}}{Q_{xx} + Q_{yy}}, \qquad e_2 = \frac{2\,Q_{xy}}{Q_{xx} + Q_{yy}}$$

They describe the **shape and orientation** of a galaxy's light distribution:

- **e1 > 0** — elongated along the x-axis (horizontal)
- **e1 < 0** — elongated along the y-axis (vertical)
- **e2 > 0** — elongated along the 45° diagonal
- **e2 < 0** — elongated along the 135° diagonal
- **e1 = e2 = 0** — perfectly round

The total ellipticity magnitude is $|e| = \sqrt{e_1^2 + e_2^2}$, and the position angle is $\phi = \frac{1}{2}\arctan(e_2 / e_1)$.

**What to expect in a catalog:**
- The *mean* of e1 and e2 over many galaxies should be ~0 (no preferred direction on a random patch of sky)
- The *RMS* is typically ~0.25–0.3, which is the **intrinsic shape noise** — galaxies are randomly oriented and have a spread of true ellipticities
- A non-zero mean or non-uniform position angle distribution can indicate **PSF systematics**

In the LSST pipeline, the HSM Regauss estimator measures e1/e2 after correcting for the PSF.
