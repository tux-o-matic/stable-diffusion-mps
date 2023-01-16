# **Stable Diffusion Dream Script**

This is a fork of a fork of
[CompVis/stable-diffusion](https://github.com/CompVis/stable-diffusion),
the open source text-to-image generator. It focuses purely on the macOS Metal backend (MPS) support and doing so without Conda and newer Python.

# **Table of Contents**

1. [Installation](#installation)
2. [Major Features](#features)
3. [Changelog](#latest-changes)
4. [Troubleshooting](#troubleshooting)

# Disclaimer
The code might be open source, what you choose to generate and eventually share might make you liable.
Generating images using stable diffusion doesn't make you an artist.

Be careful of sources used by your model. It may have been generated using protected/copyrighted material.

# Installation
This repo doesn't rely on Anaconda. It is unnecessary since other dependencies that it can't install and is more bloated than pip.

## System dependencies 
Of course Xcode with command line tools.
Then ports needed by various Python modules: 
```shell
sudo port install rust cargo protobuf-c curl-ca-bundle cmake
```
(or equivalent with HomeBrew)

This repo is tested on both Python 3.9 and 3.10, choose what works best for you:
```shell
sudo port install python310 py310-pip
```

If for some reason pip cannot find a wheel for SciPy, you will need extra ports to compile it.
```shell
sudo port install OpenBLAS gcc12 +gfortran
sudo port select --set gcc mp-gcc12
```

## Python environment
With all system depdencies installed, proceed with the project Python enivornment.
(make sure that `python3` is an alias to the right Python version you want)
```shell
git clone https://github.com/tux-o-matic/stable-diffusion-mps.git
cd stable-diffusion-mps
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
export PYTORCH_ENABLE_MPS_FALLBACK=1
export PYTHONPATH="$PYTHONPATH:$PWD/ldm/"
```
The requirements file will use other sub requimrents file. It will also force compilation of NumPy to make use of Apple's vecLib optimized for Apple Silicon instead of NumPy wheel for Darwin arm64 which lacks such optimization.


## **Hardware Requirements**

**System**

You wil need an Apple computer with Apple Silicon (not tested on Intel Mac with AMD dGPU).

**Memory**

- At least 8 GB Main Memory RAM.

**Disk**

- At least 6 GB of free disk space for the machine learning model, Python, and all its dependencies.

**Note**

Similarly, specify full-precision mode on Apple M1 hardware.

To run in full-precision mode, start `dream.py` with the
`--full_precision` flag:

```
(ldm) ~/stable-diffusion$ python scripts/dream.py --full_precision
```

# Features

## **Major Features**

- ## [Interactive Command Line Interface](docs/features/CLI.md)

- ## [Image To Image](docs/features/IMG2IMG.md)

- ## [Inpainting Support](docs/features/INPAINTING.md)

- ## [GFPGAN and Real-ESRGAN Support](docs/features/UPSCALE.md)

- ## [Seamless Tiling](docs/features/OTHER.md#seamless-tiling)

- ## [Google Colab](docs/features/OTHER.md#google-colab)

- ## [Web Server](docs/features/WEB.md)

- ## [Reading Prompts From File](docs/features/OTHER.md#reading-prompts-from-a-file)

- ## [Shortcut: Reusing Seeds](docs/features/OTHER.md#shortcuts-reusing-seeds)

- ## [Weighted Prompts](docs/features/OTHER.md#weighted-prompts)

- ## [Variations](docs/features/VARIATIONS.md)

- ## [Personalizing Text-to-Image Generation](docs/features/TEXTUAL_INVERSION.md)

- ## [Simplified API for text to image generation](docs/features/OTHER.md#simplified-api)

## **Other Features**

- ### [Creating Transparent Regions for Inpainting](docs/features/INPAINTING.md#creating-transparent-regions-for-inpainting)

- ### [Preload Models](docs/features/OTHER.md#preload-models)

# Latest Changes

- v1.14 (11 September 2022)

  - Memory optimizations for small-RAM cards. 512x512 now possible on 4 GB GPUs.
  - Full support for Apple hardware with M1 or M2 chips.
  - Add "seamless mode" for circular tiling of image. Generates beautiful effects. ([prixt](https://github.com/prixt)).
  - Inpainting support.
  - Improved web server GUI.
  - Lots of code and documentation cleanups.

- v1.13 (3 September 2022

  - Support image variations (see [VARIATIONS](docs/features/VARIATIONS.md) ([Kevin Gibbons](https://github.com/bakkot) and many contributors and reviewers)
  - Supports a Google Colab notebook for a standalone server running on Google hardware [Arturo Mendivil](https://github.com/artmen1516)
  - WebUI supports GFPGAN/ESRGAN facial reconstruction and upscaling [Kevin Gibbons](https://github.com/bakkot)
  - WebUI supports incremental display of in-progress images during generation [Kevin Gibbons](https://github.com/bakkot)
  - A new configuration file scheme that allows new models (including upcoming stable-diffusion-v1.5)
    to be added without altering the code. ([David Wager](https://github.com/maddavid12))
  - Can specify --grid on dream.py command line as the default.
  - Miscellaneous internal bug and stability fixes.
  - Works on M1 Apple hardware.
  - Multiple bug fixes.

For older changelogs, please visit **[CHANGELOGS](docs/CHANGELOG.md)**.

# Troubleshooting

Please check out our **[Q&A](docs/help/TROUBLESHOOT.md)** to get solutions for common installation problems and other issues.

# Contributing

Anyone who wishes to contribute to this project, whether documentation, features, bug fixes, code cleanup, testing, or code reviews, is very much encouraged to do so. If you are unfamiliar with
how to contribute to GitHub projects, here is a [Getting Started Guide](https://opensource.com/article/19/7/create-pull-request-github).

A full set of contribution guidelines, along with templates, are in progress, but for now the most important thing is to **make your pull request against the "development" branch**, and not against "main". This will help keep public breakage to a minimum and will allow you to propose more radical changes.

# Further Reading

Please see the original README for more information on this software
and underlying algorithm, located in the file [README-CompViz.md](docs/README-CompViz.md).
