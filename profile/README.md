# Durham Electronic Structure Group Repository

Welcome to the group repository for Durham Condensed Matter and Electronic Structure.

The purpose of this repository is to facilitate the sharing of code, potentially saving on code duplication (and duplication of efforts) as well as data files.
More importantly, it is to ensure that workflows, code and research data are not lost to the digital ether after members have left.

See below for some useful Python packages for electronic structure and contribution guidelines. **READ THESE FIRST BEFORE ADDING ANYTHING!**

## DO THIS FIRST: Git and Linux Basics
If you are unfamiliar with Git and Version Control, **please ensure you familiarise yourself with how to use it first before adding anything**.
There are countless tutorials available on how to use Git on the internet, including the [cheat sheet](https://education.github.com/git-cheat-sheet-education.pdf) from GitHub itself.

If you are unsure about anything, please ask a more senior group member!


## Some Important Repositories
- [CASTEPbands](https://github.com/NPBentley/CASTEP_bands): Visualisation of band structures and other spectral properties from CASTEP, effectively a Python library replacement to the somewhat ageing `dispersion.pl`.

  Developed initially by Zachary Hawkhead and then updated and enhanced by Nathan Bentley and Visagan Ravindran.

- [CASTEP Formatted Visualiser](https://github.com/Inker2401/castep-fmtvis): A library built on Pyvista to set up visualisation of crystal structures and 3D data.

  Although it primarily supports CASTEP, **output from other codes can also be visualised in principle**

Additionally, there is a [general scripts](https://github.com/Durham-Electronic-Structure-Group-Code/general-scripts) repository that contains miscellaneous scripts that are useful for a variety of tasks.

Finally, although an editor is a personal choice, for those who use Emacs (or would like to convert to the church of Emacs), an Emacs configuration designed for HPC and has been tested on Hamilton is available [here](https://github.com/Durham-Electronic-Structure-Group-Code/emacs-config)

## Some Useful Python Packages
Beyond the standard scientific Python ecosystem, there are some other useful libraries for electronic structure that are well-tested, mature and (mostly) stable. You should use these to benefit from the efforts of others rather than expending your own!

- The [Atomic Simulation Environment (ASE)](https://ase-lib.org/) package often can read input/output files from various electronic structure/DFT codes (including CASTEP, VASP and Quantum ESPRESSO). Other tasks like setting up supercells, fitting equations of states and more are also supported. This is also a potentially useful one to know if your workflow requires usage of multiple DFT codes.

  Note however it does not support CASTEP's arithmetic parser or unit system. In fact, bear in mind that ASE generally assumes angstroms and electronvolts for length and energy units, respectively. Be sure to do the relevant conversions before calling `ase.io.write` to create your input files!

- [Spglib](https://spglib.readthedocs.io/en/stable/) is a C library with Fortran bindings as well as a Python interface to handle space groups (including recently, magnetic space groups). ASE also requires the Python pacakge for Spglib for certain functionality.

- [PySCF](https://pyscf.org/index.html): not so much a library but a full-fledged DFT code within Python, capable of doing calculations in both periodic solids and finite systems (molecules). It is however, useful as it is capable of reading standard output files used in quantum chemistry such as `Molden` files. In addition, since it is written in Python, most of the functionality is exposed to you as an end-user and you can probably find existing functions in it to do 'standard' operations (that are otherwis tedious to code up yourself).

## Contributing Guidelines
Please pay attention to contribution guidelines that may be in the `README` or alternatively a `CONTRIBUTING.md` file.

In order to ensure portability and compatbility (think long-term!), you should ensure that your code keeps to the language standard as far as possibe. This may mean for:

- Python: stick to the standard scientific Python ecosystem  (Numpy, Scipy, matplotlib etc.) as well as the aforementioned packages.

  If you must use an other libraries/packages, please ensure you make a note of this (in the README for your script) and ideally provide a `setup.cfg` and/or `setup.py` files to allow your package
  to be installed via pip.

- Fortran:
  1. The latest standards are typically not supported by compilers straight away.
For maximum compatbility, it is recommended that you stick to the 2008 standard. Your compiler can probably check this (for instance in gfortran, one uses `-std=f2008`).

  2. **DO NOT USE IMPLICIT TYPING OR VENDOR SPECIFIC EXTENSIONS**.

  3. Create a `Makefile` if your project has a lot of dependancies.

- C++/C: Similar to Fortran. In the case of C++, target the C++20 standard.
