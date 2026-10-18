# 29P-Outburst-geometrical-model-

A Python simulation of outburst activity on comet 29P/Schwassmann-Wachmann, and a pipeline that turns about 30,000 archival photometric records into light curves, so the simulated brightness change can be compared with observations.

This is the code behind my MSc dissertation at Cardiff University (2025), supervised by Dr Paul Roche. 
## Background

29P is a centaur, a small body between Jupiter and Neptune, that brightens by up to five magnitudes in frequent, unexplained outbursts. Its nucleus shape is unknown. The model asks a simple question: if gas and dust are ejected from one site on a rotating nucleus, what does the resulting coma and brightness curve look like, and does it resemble the observed light curve?

## What is in this repo

| File | What it does |
|---|---|
| `notebooks/01_photometry_archival_data.ipynb` | Parses ten text files of archival observation records (2015 to April 2025), converts dates to Julian Date, separates the filter code, selects R-band entries, and plots the light curve and its brightness gradient |
| `notebooks/02_particle_ejection_model.ipynb` | Builds the model in stages: jet geometry on a rotating nucleus, then a particle-ejection model with gravity, escape velocity, nucleus rotation and brightness. Final scenarios: a single outburst and five outbursts |

## Results

- Single outburst: 50,000 particles ejected over 15 minutes. Simulated brightness rise of about 1.67 x 10^-4 mag/s.
- Five outbursts (placed to match JWST observations): about 10^6 particles in total. Simulated rise of about 1.33 x 10^-4 mag/s.
- Observed rise in the archival light curve: about 0.23 x 10^-4 mag/s.

The simulated outbursts show the same behaviour as the observed ones, but the simulated brightening is steeper and much smaller in total.

## Limitations

These are also stated in the paper.

- The nucleus is assumed to be spherical, because no shape data exist for 29P.
- Nucleus density is taken from comet 67P, the only comet where it has been measured accurately.
- The simulation reached 10^6 particles before running out of memory. Realistic numbers are 10^10 to 10^12, so a scale factor is applied to the brightness. It cannot fully represent the true cross-sectional area.
- The R-band selection leaves out the 2015 file, which has no filter information.

## How to run

```
pip install numpy pandas scipy matplotlib astropy plotly pillow
```

1. Put the observation files in a folder called `data/` next to the notebooks (`29P_2015.txt`, `29P_2016.txt`, ... `29P_2024-25.txt`). The raw files are not included here; see Data below.
2. Run `01_photometry_archival_data.ipynb` from top to bottom.
3. Run `02_particle_ejection_model.ipynb`. It saves animations to an `outputs/` folder it creates.

The particle model uses random numbers without a fixed seed, so each run gives slightly different particles.

## Data

The observation records come from public archives cited in the paper (Las Cumbres Observatory and the British Astronomical Association). They are not redistributed in this repo.

## Paper

*Investigating 29P/Schwassmann-Wachmann and modelling its unique outburst activity.* Spyrou, Roche, O'Sullivan. Cardiff University.
