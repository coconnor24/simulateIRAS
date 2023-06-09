# simulateIRAS
## Description
A python package for simulating spectra and determining extinction coefficients (k parameters) for polarization- and azimuth-resolved infrared reflection absorption spectroscopy (IRAS) measurements for non-magnetic substrates. The current simulations utilize a three-layer (vacuum-adsorbate-substrate) model derived according to [1] and implemented in [2].
<br> <br> <br>
<img src='./images/IRAS_Model_3_Layer.png' width='50%'>
<br> <br>
The three-layer (vacuum-adsorbate-substrate) model for light incident along the xz plane of a substrate in the xy plane gives:
<br>
$${\frac{\Delta R}{R}} \vert_{(s-pol)} = 8 \ \pi \ \tilde{\nu} \ d \ \sqrt{\epsilon^{s}\_{y}} \ cos(\phi) \ Im(\frac{\epsilon^{s}\_{y} \ - \ \tilde{\epsilon}^{a}\_{y}}{\epsilon^{s}\_{y} \ - \ \epsilon^{v}})$$
<br>
$${\frac{\Delta R}{R}} \vert_{(p-pol)} = 8 \ \pi \ \tilde{\nu} \ d \ \sqrt{\epsilon^{s}\_{y}} \ cos(\phi) \ Im(\frac{\alpha}{\beta})$$
$$\alpha = (\epsilon^{s}\_{x} \ - \ \tilde{\epsilon}^{a}\_{x}) - (\frac{\epsilon^{s}\_{x}}{\tilde{\epsilon}^{a}\_{z}} \  - \ \frac{\tilde{\epsilon}^{a}\_{x}}{\epsilon^{s}\_{z}}) \ {\epsilon^{v}} \ sin^{2}(\phi)$$
$$\beta = (\epsilon^{s}\_{x} \ - \ \epsilon^{v}) - (\frac{\epsilon^{s}\_{x}}{\tilde{\epsilon}^{v}} \  - \ \frac{\epsilon^{v}}{\epsilon^{s}\_{z}}) \ {\epsilon^{v}} \ sin^{2}(\phi)$$
<br>
Where: <br>
$\tilde{\nu} =$ wavenumber <br>
$d =$ adsorbate film thickness (approximate for coverage) <br>
$\phi =$ angle of light incidence with respect to the surface normal direction <br>
$\epsilon^{s}\_{x} =$ dielectric constant of the substrate layer along the x-axis (in substrate plane along incident light) <br>
$\epsilon^{s}\_{y} =$ dielectric constant of the substrate layer along the y-axis (in substrate plane orthogonal to incident light) <br>
$\epsilon^{s}\_{z} =$ dielectric constant of the substrate layer along the z-axis (normal to substrate plane) <br>
$\epsilon^{a}\_{x} =$ dielectric constant of the adsorbate film along the x-axis (in substrate plane along incident light) <br>
$\epsilon^{a}\_{y} =$ dielectric constant of the adsorbate film  along the y-axis (in substrate plane orthogonal to incident light) <br>
$\epsilon^{a}\_{z} =$ dielectric constant of the adsorbate film  along the z-axis (normal to substrate plane) <br>
$\epsilon^{v} =$ dielectric constant of the vacuum which is isotropic <br>
$\tilde{\epsilon}^{i}\_{j} =$ a complex dielectric constant for layer i along axis j
<br>
<br>
The complex index of refraction is related to the complex dielectric constant by: <br>
$$\tilde{\epsilon}^{i}\_{j} = (\tilde{n}^{i}\_{j})^{2}$$ <br>
<br>
Where: <br>
$\tilde{n} =$ complex index of fraction for layer i along axis j<br>
$\tilde{\epsilon}^{i}\_{j} =$ complex dielectric constant for layer i along axis j<br>
<br>
<br>
The extinction coefficient (k parameters) is related to the complex index of refraction by: <br>
$$k^{i}\_{j} = Im(\tilde{n}^{i}\_{j})$$ <br>
<br>
Where: <br>
$\tilde{n} =$ complex index of fraction for layer i along axis j<br>
$k^{i}\_{j} =$ the extinction coefficient (k parameter) for layer i along axis j<br>
<br>

## Installation
The python package can be installed via PyPI (pip):
<br><br>
`pip install simulateIRAS` 
<br><br>
We recommend importing in python as iras. 
<br><br>
`import simulateIRAS as iras`
<br>

## Examples
### Example 1: Simulating polarization- and azimuth-resolved IRAS spectra
This example simulates the 4 polarization- and azimuth-resolved IRAS spectra with given k parameters k(x), k(y), k(z) for an adsorbate film on an isotropic, dielectric substrate. The python code, input files and output files are provided in "simulateIRAS/examples/simpleSimulation". The simulation requires the following inputs: 
1) incident angle of light relative to the surface normal
2) complex index of refraction of the substrate layer which here is wavelength independent for an isotropic substrate modelling anatase TiO<sub>2</sub>(101) as $n = 2.3 + 0.0i$
3) k parameters of the adsorbate layer (imaginary part of the complex index of refraction) which here is for a deuterated water film
4) real index of refraction of the adsorbate layer in the infinite wavenumber simulation limit which here is taken as $Real(n) = 1.37$ for a deuterated water film
5) adsorbate film thickness
<br>
The Kramers–Kronig relations are used on the adsorbate k parameters (imaginary part of the complex index of refraction) to get the real part of the complex index of refraction for the adsorbate layer. The simulation then applies the three-layer (substrate-adsorbate-vacuum) model to simulate the 4 polarization- and azimuth-resolved IRAS spectra.
<br>
<br>
The input adsorbate k parameters and 4 polarization- and azimuth-resolved simulated IRAS spectra are plotted below:
<br>
<br>
<p align="center">
<img src='./examples/simpleSimulation/Solutions/Figure0.png' width='40%'><img src='./examples/simpleSimulation/Solutions/Figure1.png' width='40%'>
</p>

### Example 2: Determining extinction coefficients from polarization- and azimuth-resolved IRAS spectra
This example regresses the adsorbate k parameters k(x), k(y), k(y) by comparing the 4 polarization- and azimuth-resolved simulated and experimental IRAS spectra for an adsorbate film on isotropic, dielectric substrate. The python code, input files and output files are provided in "simulateIRAS/examples/dataRegression". The simulation requires the following inputs: 
1) 4 polarization- and azimuth-resolved IRAS spectra
2) incident angle of light relative to the surface normal
3) complex index of refraction of the substrate layer which here is wavelength independent for an isotropic substrate modelling anatase TiO<sub>2</sub>(101) as $n = 2.3 + 0.0i$
4) real index of refraction of the adsorbate layer in the infinite wavenumber simulation limit which here is taken as $Real(n) = 1.37$ for a deuterated water film
5) adsorbate film thickness
<br>
The Kramers–Kronig relations are used on the regressed adsorbate k parameters (imaginary part of the complex index of refraction) to get the real part of the complex index of refraction for the adsorbate layer. The simulation then applies the three-layer (substrate-adsorbate-vacuum) model to simulate the 4 polarization- and azimuth-resolved IRAS spectra. First, the simulation regresses the adsorbate k(y) and k(x) parameters to the s(y) and s(x) experimental IRAS spectra. Second, the simulation regresses the adsorbate k(z) parameters to the p(xz) and p(yz) experimental IRAS spectra. For these two steps, the regression works by adding to k(i) a Lorentzian (FWHM = 1) with a random position, small amplitude and sign and only accepting the new k(i) if the fit to the spectra(s) is better. Finally, the simulation regresses the adsorbate k(x), k(y) and k(z) parameters to fits of all the s(y), p(xz), s(x), p(yz) experimental IRAS spectra. For this step, the regression works by adding to a random k(i) a Lorentzian (FWHM = 1) with a random position, small amplitude and sign and only accepting the new k(i) if the total fit to all 4 spectra is better. For all regression steps there is a cutoff parameter which determines how much better a fit needs to be in order for the new test k(i) parameter to be accepted.
<br>
<br>
The regressed adsorbate k parameters and 4 polarization- and azimuth-resolved (solid) simulated and (dots) experimental IRAS spectra are plotted below:
<br>
<br>

<p align="center">
<img src='./examples/dataRegression/Solutions/Figure0.png' width='40%'><img src='./examples/dataRegression/Solutions/Figure1.png' width='40%'>
</p>

## References
[1] Chabal YJ (1987) Vibrational Properties at Semiconductor Surfaces and Interfaces. In: Le Lay G, Derrien J, Boccara N (eds) Semiconductor Interfaces: Formation and Properties. Springer Berlin Heidelberg, Berlin, Heidelberg
<br>
[2] O'Connor et al. In preparation.
