# APCEMM

[![DOI](https://zenodo.org/badge/256520978.svg)](https://zenodo.org/badge/latestdoi/256520978)

APCEMM is the [Aircraft Plume Chemistry, Emissions, and Microphysics Model](https://github.com/mit-lae/APCEMM). It simulates the aerosol microphysics and chemistry in an aircraft exhaust plume in 2D for up to 24 hours, with a focus on accurate simulation of the ice - providing an intermediate-fidelity representation of an aircraft contrail. Originally described in [Fritz et al. (2020)](https://acp.copernicus.org/articles/20/5697/2020/), the model has since been heavily modified and the focus shifted from chemistry towards a flexible and efficient contrail simulation. APCEMM is a community-developed code and we strongly encourage users to contribute to the code base, whether through new features, improvements, or bug fixes. We use semantic versioning, and (as of v1.1.0) users can expect that the API will only change with new major versions.

The latest stable release of APCEMM is [__v1.2.0__](https://github.com/MIT-LAE/APCEMM/releases/tag/v1.2.0).

## APCEMM development

The development of APCEMM in C++ started in September 2018. The most recent version of the code can be found in the __main__ branch. Although usually functional, this code is not necessarily stable and new features are added to this branch relatively frequently.

For __users__ of APCEMM who do not intend to do any development, we recommend downloading a recent stable version. To acquire (for example) version 1.2.0, use `git checkout v1.2.0` after cloning the repository.
For __developers__ of APCEMM, we ask that you create a fork of this repository. Any user can contribute to APCEMM - see ["contributing to APCEMM"](community.md#contributing).

For VSCode users, a Docker Dev Container is defined in `.devcontainer`. See [the tutorial](https://code.visualstudio.com/docs/devcontainers/tutorial) to develop inside a containerized environment.
