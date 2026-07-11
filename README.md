# Awesome Radio Astronomy [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated list of open data archives, surveys, software, papers, telescopes, and learning resources for radio astronomy.

Compiled from the [**jansky**](https://github.com/joebarbere/jansky) course (a hands-on radio-astronomy course in Python) and its research sibling [**jansky-research**](https://github.com/joebarbere/jansky-research) (reproducible amateur-research "slices" → honest papers). Everything here is something one of those projects actually uses, cites, or builds on — biased toward **open, no-authentication, programmatically accessible** resources an independent researcher can use today.

## Contents

- [Data archives & catalogues](#data-archives--catalogues)
- [Surveys & instruments](#surveys--instruments)
- [Software & libraries](#software--libraries)
  - [Core stack](#core-stack)
  - [Pulsars & timing](#pulsars--timing)
  - [SETI](#seti)
  - [FRBs & transients](#frbs--transients)
  - [Interferometry, imaging & formats](#interferometry-imaging--formats)
  - [Data engineering & reproducibility](#data-engineering--reproducibility)
  - [Solar, planetary & sky models](#solar-planetary--sky-models)
- [Telescopes & observatories](#telescopes--observatories)
- [Key papers & textbooks](#key-papers--textbooks)
- [Learning resources](#learning-resources)
- [Contributing](#contributing)

## Data archives & catalogues

Public, bulk-accessible archives — most of these are queryable from Python.

- [VizieR](https://vizier.cds.unistra.fr/) — CDS catalogue service; hosts NVSS (`VIII/65`), the ATNF pulsar catalogue (`B/psr`), the Taylor+2009 RM catalogue (`J/ApJ/702/1230`), GLEAM-X, GLEAM, SUMSS, FIRST, LoTSS DR2 (`J/A+A/659/A1`), and tens of thousands more. The backbone of catalogue-level research.
- [NASA SPDF / CDAWeb](https://spdf.gsfc.nasa.gov/) — Space Physics Data Facility; public, no-auth heliospheric radio data (Wind/WAVES L2 CDFs, STEREO/WAVES one-minute HFR ASCII, STEREO/WAVES L3 goniopolarimetric direction-finding CDFs).
- [CADC / CIRADA VLASS catalogues](https://cirada.ca/catalogues) — VLASS Quick-Look component catalogues (~3.4M components/epoch); Single-Epoch images via CADC SODA cutouts.
- [CASDA — CSIRO ASKAP Science Data Archive](https://data.csiro.au/domain/casdaObservation) — ASKAP data including all three RACS bands and VAST; TAP via `astroquery.casda`, SODA cutouts, free OPAL account.
- [Astrogeo VLBI image database](http://astrogeo.org/) — ~150k dual-band S/X (2.3/8.4 GHz) VLBI images of ~21k compact sources from decades of geodetic/astrometric VLBI (L. Petrov); the largest public VLBI image archive, with multi-decade per-source flux histories.
- [e-Callisto](http://www.e-callisto.org/) — global network of ground-based solar radio spectrometers (~20–900 MHz, 15-minute FITS), 150+ stations, 20+ years ([data tree](http://soleil.i4ds.ch/solarradio/data/2002-20yy_Callisto/)).
- [Breakthrough Listen Open Data](http://seti.berkeley.edu/opendata) — professional-grade GBT/Parkes/MeerKAT bulk SETI data; includes the canonical [Voyager 1 fine-resolution recording](http://blpd0.ssl.berkeley.edu/Voyager_data/).
- [LOFAR LoTSS / LTA](https://lofar-surveys.org/) — LoTSS DR2/DR3 catalogues (DR3 ≈ 13.7M sources over 88% of the northern sky) and the LOFAR Long-Term Archive.
- [NRAO Science Data Archive](https://data.nrao.edu/) — VLA / VLBA / GBT archival visibilities and images.
- [HEASARC](https://heasarc.gsfc.nasa.gov/) — NASA's high-energy archive, for multiwavelength X-ray context.
- [NASA LAMBDA](https://lambda.gsfc.nasa.gov/) — CMB and foreground data; hosts the HI4PI all-sky N_HI HEALPix map.
- [Planck Legacy Archive](https://pla.esac.esa.int/) — ESA Planck temperature/polarisation and radio-foreground maps.
- [CHIME/FRB catalogue](https://www.chime-frb.ca/catalog) — Catalog 1 public CSV (DM, fluence, width, repeater name).
- [ATNF Pulsar Catalogue (psrcat)](https://www.atnf.csiro.au/research/pulsar/psrcat/) — periods, period derivatives, and flux densities for the known pulsars.
- [SIMBAD](https://simbad.cds.unistra.fr/) & [NED](https://ned.ipac.caltech.edu/) — source identification and cross-match for candidate vetting.
- [MASER / Paris Observatory](https://maser.obspm.fr/) — planetary & solar radio (Cassini RPWS, Juno Waves, Voyager PRA, Radio JOVE CDFs).
- [Radio JOVE archive](https://radiojove.net/archive/) — amateur/citizen-science Jovian and decametric recordings.
- [Gaia Archive](https://gea.esac.esa.int/archive/) — optical astrometry; cross-matched with ICRF3 for radio–optical position offsets.
- [MWA ASVO](https://asvo.mwatelescope.org/) — MWA node of the All-Sky Virtual Observatory to browse the full MWA observation history and download public visibility data (incl. GLEAM); free account required for downloads.
- [LWA Data Archive](https://lda10g.alliance.unm.edu/) — public archive of the Long Wavelength Array (10–88 MHz): pulsar data, PASI/Orville all-sky images, and the LWA1 Low Frequency Sky Survey maps.
- [Pulsar Survey Scraper](https://pulsar.cgca-hub.org/) — aggregates recent pulsar discoveries from 35+ surveys ahead of psrcat, searchable by position/DM via web UI and JSON API.
- [FRBSTATS](https://www.herta-experiment.org/frbstats/) — open, continuously updated FRB catalogue with DM-inferred redshifts, a public REST API, and CSV/JSON export.
- [RMTable — consolidated Faraday RM catalogue](https://github.com/CIRADA-Tools/RMTable) — CIRADA's standardised, machine-readable catalogue of ~59,500 published rotation measures (FITS/TSV/VOTable) with a Python reader.
- [NANOGrav Data Releases](https://nanograv.org/science/data) — public pulsar-timing-array datasets (TOAs and `.par`/`.tim` timing models for tempo2/PINT) from the 5- to 15-year releases, hosted on Zenodo.
- [ALMA Science Archive](https://almascience.org/aq/) — query interface plus VO TAP/SIA endpoints for all public ALMA mm/submm interferometric data, accessible anonymously from pyvo/astroquery.

## Surveys & instruments

Survey **products** are mostly reached through the archives above; this is the field guide to what each one is.

- **NVSS** — NRAO VLA Sky Survey, 1.4 GHz, ~1.8M sources north of Dec −40° (Condon et al. 1998).
- **FIRST** — VLA 1.4 GHz, deep high-resolution imaging (Becker, White & Helfand 1995).
- **VLASS** — VLA Sky Survey, 2–4 GHz, 2.5″, three epochs 2017–2024; Quick-Look + Single-Epoch.
- **TGSS ADR1** — GMRT 150 MHz all-sky low-frequency survey (Intema et al. 2017).
- **GLEAM / GLEAM-X** — MWA 72–231 MHz; GLEAM-X DR2 gives 20 in-band sub-bands (Hurley-Walker; Ross et al. 2024).
- **RACS** — Rapid ASKAP Continuum Survey, three bands (887.5 / 1367.5 / 1655.5 MHz), incl. Stokes V.
- **VAST** — Variables And Slow Transients (ASKAP) light curves.
- **SUMSS** — Sydney University Molonglo Sky Survey, 843 MHz southern.
- **LAB / HI4PI** — Leiden/Argentine/Bonn and HI4PI all-sky neutral-hydrogen 21 cm surveys.
- **CHIME/FRB** — 400–800 MHz transit interferometer; the most prolific FRB catalogue.
- **Wind/WAVES & STEREO/WAVES** — space-based interplanetary radio (RAD1/RAD2 0.02–14 MHz; HFR 0.125–16 MHz; STEREO L3 direction-finding).
- **ICRF3 & Gaia DR3** — the radio (VLBI) and optical celestial reference frames.

## Software & libraries

### Core stack

- [Astropy](https://www.astropy.org/) — the core astronomy library (units, coordinates, FITS, tables, cosmology).
- [Astroquery](https://astroquery.readthedocs.io/) — VO and archive queries (VizieR, SIMBAD, NED, `astroquery.casda`, …).
- [PyVO](https://pyvo.readthedocs.io/) — Virtual Observatory / TAP access.
- [spectral-cube & radio-beam](https://radio-astro-tools.github.io/) — spectral-cube handling and beam arithmetic.
- [NumPy](https://numpy.org/) · [SciPy](https://scipy.org/) · [Matplotlib](https://matplotlib.org/) — the numerical and plotting base.
- [healpy](https://healpy.readthedocs.io/) — HEALPix all-sky maps (CMB/foregrounds).

### Pulsars & timing

- [PINT](https://github.com/nanograv/PINT) — modern, Python-native pulsar timing.
- [PRESTO](https://github.com/scottransom/presto) — the classic CPU pulsar search suite.
- [your](https://github.com/thepetabyteproject/your) — unified PSRFITS/filterbank I/O.
- [TEMPO2](https://bitbucket.org/psrsoft/tempo2) — the standard pulsar-timing package.
- [enterprise](https://github.com/nanograv/enterprise) — Bayesian pulsar-timing-array analysis.
- [libstempo](https://github.com/vallis/libstempo) — Python wrapper around TEMPO2 and the numerical backend behind enterprise.
- [clfd](https://github.com/v-morello/clfd) — automated “clean folded data” RFI cleaning for pulsar search and timing archives.
- [riptide](https://github.com/v-morello/riptide) — Fast Folding Algorithm implementation for detecting long-period pulsars.
- [PulsarX](https://github.com/ypmen/PulsarX) — high-performance pulsar search pipeline (dedispersion, folding, RFI mitigation) for filterbank/PSRFITS.
- [sigpyproc3](https://github.com/FRBs/sigpyproc3) — modern Python 3 library for reading and processing SIGPROC filterbank and time-series data.

### SETI

- [blimpy](https://github.com/UCBerkeleySETI/blimpy) — Breakthrough Listen filterbank/HDF5 I/O.
- [turboSETI](https://github.com/UCBerkeleySETI/turbo_seti) — Doppler-drift narrowband search (Taylor tree).
- [setigen](https://github.com/bbrzycki/setigen) — synthetic narrowband-signal injection.
- [seticore](https://github.com/lacker/seticore) — high-performance C++/GPU implementation of core SETI dedoppler/beamforming algorithms, deployed at MeerKAT/VLA.

### FRBs & transients

- [frbpoppy](https://github.com/TRASAL/frbpoppy) — FRB population synthesis (also vendors the CHIME Cat-1 CSV).
- [Heimdall](https://sourceforge.net/projects/heimdall-astro/) — GPU single-pulse / FRB de-dispersion search.
- [FETCH](https://github.com/devanshkv/fetch) — deep-learning FRB candidate classification.
- [DM_phase](https://github.com/danielemichilli/DM_phase) — determines the structure-maximising dispersion measure of a burst using coherent phase information.
- [TransientX](https://github.com/ypmen/TransientX) — high-performance single-pulse / transient search pipeline with DBSCAN candidate clustering.
- [fitburst](https://github.com/CHIMEFRB/fitburst) — CHIME/FRB toolkit for forward-modelling FRB dynamic spectra (width, scattering, drift).

### Interferometry, imaging & formats

- [CASA](https://casa.nrao.edu/) — calibration and imaging of Measurement Sets.
- [WSClean](https://gitlab.com/aroffringa/wsclean) — fast wide-field interferometric imager.
- [PyBDSF](https://github.com/lofar-astron/PyBDSF) — radio source finding.
- [Aegean](https://github.com/PaulHancock/Aegean) — compact-source finder.
- [pyuvdata](https://github.com/RadioAstronomySoftwareGroup/pyuvdata) — visibility format interchange (MS ↔ UVFITS ↔ UVH5).
- [AOFlagger](https://gitlab.com/aroffringa/aoflagger) — RFI flagging.
- [SigMF](https://github.com/sigmf/SigMF) — portable SDR-recording metadata format.
- [GNU Radio](https://www.gnuradio.org/) — SDR signal-processing flowgraphs.
- [ducc](https://github.com/mreineck/ducc) — efficient numerical kernels including the non-uniform FFT gridder (“nifty-gridder”) used by WSClean.
- [eht-imaging](https://github.com/achael/eht-imaging) — regularised-maximum-likelihood VLBI imaging and analysis library used by the Event Horizon Telescope.
- [CARTA](https://cartavis.org/) — browser-based viewer/analyser for large radio image cubes (ALMA/VLA/SKA-pathfinder scale).
- [DP3](https://github.com/lofar-astron/DP3) — streaming preprocessing/calibration pipeline for interferometric data (averaging, flagging, gain calibration); core LOFAR tool.
- [python-casacore](https://github.com/casacore/python-casacore) — Python bindings to casacore for reading/writing Measurement Sets, images, and tables outside CASA.

### Data engineering & reproducibility

- [cdflib](https://github.com/MAVENSDC/cdflib) — pure-Python CDF reader (Wind/WAVES, STEREO/WAVES).
- [Snakemake](https://snakemake.readthedocs.io/) — server-less file-target workflow DAGs (right for static, reproducible pipelines).
- [Apache Airflow](https://airflow.apache.org/) — scheduled, backfilling orchestration (right for frequently-updated streaming archives).
- [Podman](https://podman.io/) — daemonless, rootless container runtime.
- [Tectonic](https://tectonic-typesetting.github.io/) — self-contained, reproducible LaTeX engine for paper builds.
- [ASCL — Astrophysics Source Code Library](https://ascl.net/) — the field's software index.

### Solar, planetary & sky models

- [SunPy](https://github.com/sunpy/sunpy) — the core Python package for solar physics data (maps, timeseries, coordinate frames, search).
- [radiospectra](https://github.com/sunpy/radiospectra) — SunPy-affiliated reader/analyser for solar radio dynamic spectra (e.g. e-Callisto).
- [pyGDSM](https://github.com/telegraphic/pygdsm) — Python interface to Global Diffuse Sky Models of the radio sky (10 MHz–5 THz) for foreground/sky-temperature prediction.

## Telescopes & observatories

The jansky course ships a [full catalogue of 40 facilities](https://github.com/joebarbere/jansky/blob/main/docs/telescopes.md) (with specs and a downloadable `telescopes.kml`). Selected highlights:

**Large single dishes** — [FAST](https://fast.bao.ac.cn/) (500 m) · [GBT](https://greenbankobservatory.org/telescopes/gbt/) (100 m) · [Effelsberg](https://www.mpifr-bonn.mpg.de/en/effelsberg) (100 m) · [Parkes "Murriyang"](https://www.atnf.csiro.au/about/facilities/parkes.html) (64 m) · [Lovell / Jodrell Bank](https://www.jodrellbank.manchester.ac.uk/) (76 m).

**Interferometers & arrays** — [Karl G. Jansky VLA](https://public.nrao.edu/telescopes/vla/) · [ALMA](https://www.almaobservatory.org/) · [ATCA](https://www.narrabri.atnf.csiro.au/) · [GMRT/uGMRT](http://www.gmrt.ncra.tifr.res.in/) · [CHIME](https://chime-experiment.ca/) · [MeerKAT](https://www.sarao.ac.za/science/meerkat/) · [ASKAP](https://www.csiro.au/en/about/facilities-collections/atnf/askap-radio-telescope) · [MWA](https://www.mwatelescope.org/) · [LOFAR](https://www.astron.nl/telescopes/lofar/) · [SKAO](https://www.skao.int/).

**VLBI networks** — [VLBA](https://public.nrao.edu/telescopes/vlba/) · [EVN](https://www.evlbi.org/) · [Event Horizon Telescope](https://eventhorizontelescope.org/) · [Long Baseline Array](https://www.atnf.csiro.au/about/facilities/lba.html).

## Key papers & textbooks

The course maintains two link-verified bibliographies — pull the full lists from them:

- [`docs/references.md`](https://github.com/joebarbere/jansky/blob/main/docs/references.md) — seminal papers grouped by theme, each with an ADS/DOI link. Founding works: [Jansky 1933](https://ui.adsabs.harvard.edu/abs/1933PIRE...21.1387J), [Reber 1944](https://doi.org/10.1086/144668), [Ewen & Purcell 1951 (HI line)](https://doi.org/10.1038/168356a0), [Hewish et al. 1968 (pulsars)](https://doi.org/10.1038/217709a0), [Högbom 1974 (CLEAN)](https://ui.adsabs.harvard.edu/abs/1974A%26AS...15..417H), [Condon et al. 1998 (NVSS)](https://doi.org/10.1086/300337).
- [`docs/papers-timeline.md`](https://github.com/joebarbere/jansky/blob/main/docs/papers-timeline.md) — a year-by-year chronology of the field (1932 → today).

**Standing textbooks**

- [Condon & Ransom, *Essential Radio Astronomy*](https://science.nrao.edu/opportunities/courses/era) — the best free companion text.
- [Thompson, Moran & Swenson, *Interferometry and Synthesis in Radio Astronomy*](https://link.springer.com/book/10.1007/978-3-319-44431-4) — the interferometry standard (open access).
- Wilson, Rohlfs & Hüttemeister, *Tools of Radio Astronomy*.
- Pacholczyk, *Radio Astrophysics* — synchrotron and minimum-energy arguments.

## Learning resources

- [**jansky**](https://joebarbere.github.io/jansky/) — a hands-on radio-astronomy course in Python: runnable Jupyter chapters (prose + physics + code + plots), a tested helper package, and an MkDocs site. Arc: emission physics → signals/noise/the radiometer equation → antennas/receivers/SDR → the hydrogen line → interferometry & aperture synthesis → CLEAN → pulsars → FRBs → VLBI/EHT → pulsar-timing arrays → SETI → CMB → solar & planetary radio → polarisation & Faraday rotation → RFI mitigation → source counts & radio galaxies.
- [**jansky-research**](https://github.com/joebarbere/jansky-research) — reproducible amateur-research "slices" → AASTeX papers, each reusing the course as a library: FRB statistics & periodicity, SETI drift search, HI rotation curve, Euclidean source counts, peaked/steep-spectrum selection, pulsar spectra & the P–Ṗ diagram, the Galactic Faraday rotation sky, VLBI & VLASS variability, image-plane stacking, radio–optical offsets, and a family of solar type III burst studies (drift-to-distance, 3D triangulation, corona → 0.4 AU synthesis).
- [Essential Radio Astronomy (NRAO course)](https://science.nrao.edu/opportunities/courses/era) — the canonical free online course.
- [SARA — Society of Amateur Radio Astronomers](https://radio-astronomy.org/) — journal, [getting-started guide](https://radio-astronomy.org/getting-started), and article index.
- [jansky glossary](https://github.com/joebarbere/jansky/blob/main/docs/glossary.md) — ~160 key terms, from *aperture synthesis* and *brightness temperature* to *rotation measure* and *the Macquart relation*.
- [jansky data-formats reference](https://github.com/joebarbere/jansky/blob/main/docs/data-formats.md) — GUPPI raw, SIGPROC filterbank, PSRFITS, Measurement Set, UVFITS/UVH5, SigMF — what each holds and what reads it.

## Contributing

Contributions welcome — see [`CONTRIBUTING.md`](CONTRIBUTING.md). In short: one resource per pull request, keep entries to a single line (`[Name](url) — what it is and why it's useful`), prefer open and programmatically accessible resources, and place each item in the most specific section.

## License

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](LICENSE)

To the extent possible under law, the contributors have waived all copyright and related rights to this work ([CC0 1.0](LICENSE)).
