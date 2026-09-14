# CLASS MAD: Millicharged Atomic Dark Matter in CLASS

This is a modified version of the Boltzmann code [CLASS](http://class-code.net),
built on top of [CLASS ADM](https://github.com/jp-barron/class_adm-3.1)
by Jared Barron and collaborators. CLASS ADM adds a "twin" dark sector made of
atomic dark matter (a dark proton, a dark electron and a dark photon) with its
own recombination history. CLASS MAD extends it with elastic scattering between
the dark sector particles and Standard Model baryons, as arises for instance
from a dark-photon kinetic mixing (millicharged atomic dark matter).

The Standard Model part of the code is unchanged with respect to CLASS
version 3.1 and is documented in the original [README](README.md) and on the
[CLASS wiki](https://github.com/lesgourg/class_public/wiki).

## What is new with respect to CLASS ADM

- Momentum and heat exchange between dark protons, dark electrons and SM
  protons and electrons, with a velocity-dependent cross section (index n = -4),
  in both the thermodynamics and the perturbation modules.
- A tight-coupling treatment of the baryon–dark-matter drag that remains
  numerically stable when the drag rate is large, following the approach of
  the `dmeff` branch of CLASS.
- Derived quantities exposed through the Python wrapper, including the
  inferred dark-matter millicharge.

## Installation

Same as CLASS. See the original README for compilers and the Python wrapper.
The `tau_reio` input is not supported in this version; use `z_reio` instead.

## New input parameters

The full list, with comments and default values, is in
[`explanatory_mad.ini`](explanatory_mad.ini). In short:

Twin sector (inherited from CLASS ADM):

| parameter | meaning |
|---|---|
| `r_all_twin` | fraction of the dark matter that is atomic dark matter (0 to 1) |
| `Delta_N_twin` | contribution of the dark radiation to N_eff |
| `m_p_dark`, `m_e_dark` | dark proton and dark electron masses in GeV |
| `alphafs_dark` | dark fine-structure constant |
| `YHe_twin` | dark helium mass fraction |

Dark-matter–baryon scattering (new):

| parameter | meaning |
|---|---|
| `cross_idm_b` | dark-proton–proton cross section in cm^2; the other channels scale with the reduced masses |
| `log10_cross_idm_b` | same, as log10 |
| `log10_ratio_idm_b` | alternative: log10 of the ratio of the DM–SM to the DM–dark-radiation Compton rate at dark decoupling; the cross section is inferred |
| `flag_pD_p`, `flag_pD_e`, `flag_eD_p`, `flag_eD_e` | switch each of the four scattering channels on (1) or off (0); default all on |
| `n_index_idm_b` | velocity-dependence index of the cross section; only -4 is implemented |

Only one of `cross_idm_b`, `log10_cross_idm_b` and `log10_ratio_idm_b` may be
given. Scattering requires the twin sector to be on (`r_all_twin > 0`).

## Citing

If you use this code, please cite:

- the CLASS MAD paper: *Vanzan, Boddy, Kovetz*, **[arXiv:XXXX.XXXXX]**
- the CLASS ADM paper: *Bansal, Barron, Curtin, Tsai*,
  [arXiv:2212.02487](https://arxiv.org/abs/2212.02487)
- CLASS itself: Blas, Lesgourgues, Tram, *CLASS II: Approximation schemes*,
  [arXiv:1104.2933](http://arxiv.org/abs/1104.2933)
