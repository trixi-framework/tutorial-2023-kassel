# Trixi.jl: High-Order Numerical Simulations of Conservation Laws in Julia

This is the companion repository for the online tutorial on the
[Julia programming language](https://julialang.org) and
[Trixi.jl](https://github.com/trixi-framework/Trixi.jl), given in the context of
the DFG research unit [SNuBIC](https://snubic.io) on 19th January 2023.

In case of questions before the beginning of the tutorial, please get in touch with
[Michael](https://lakemper.eu) or
[create an issue](https://github.com/trixi-framework/tutorial-2023-snubic/issues/new).
For Trixi.jl-specific questions, you can also create an issue in the
[Trixi.jl GitHub repository](https://github.com/trixi-framework/Trixi.jl)
or
[join the Trixi.jl Slack workspace](https://join.slack.com/t/trixi-framework/shared_invite/zt-sgkc6ppw-6OXJqZAD5SPjBYqLd8MU~g).


## Tutorial files
| Item | [nbviewer](https://nbviewer.jupyter.org/) | [mybinder](https://mybinder.org/) |
|:-|:-:|:-:|
| [`introduction_to_julia.ipynb`](introduction_to_julia.ipynb) | [![nbviewer](https://raw.githubusercontent.com/jupyter/design/master/logos/Badges/nbviewer_badge.svg)](https://nbviewer.jupyter.org/github/trixi-framework/tutorial-2023-snubic/blob/main/introduction_to_julia.ipynb) | [![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/trixi-framework/tutorial-2023-snubic/HEAD?filepath=introduction_to_julia.ipynb) |
| [`introduction_to_trixi.ipynb`](introduction_to_trixi.ipynb) | [![nbviewer](https://raw.githubusercontent.com/jupyter/design/master/logos/Badges/nbviewer_badge.svg)](https://nbviewer.jupyter.org/github/trixi-framework/tutorial-2023-snubic/blob/main/introduction_to_trixi.ipynb) | [![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/trixi-framework/tutorial-2023-snubic/HEAD?filepath=introduction_to_trixi.ipynb) |

**Note: The Jupyter notebook files will be provided at the latest on the day of the
tutorial.** You can, however, already follow the instructions
below to
[set up a local Julia/Jupyter installation](#setting-up-a-local-juliajupyter-installation),
including installing Julia/IJulia and the required Julia packages.

Additional tutorials are available in the
[documentation of Trixi.jl](https://trixi-framework.github.io/Trixi.jl/stable/).


## Abstract

Trixi.jl is a numerical simulation framework for adaptive, high-order
discretizations of conservation laws. It has a modular architecture that
allows users to easily extend its functionality and was designed to be
useful to experienced researchers and new users alike.
In this two-part tutorial, we will first give a brief introduction to the
Julia programming language. In the second part, we will
demonstrate what you can do with Trixi.jl and how you can use it (and extend it)
for your own research. You can follow the tutorials interactively
using reproducible Jupyter notebooks provided in a companion repository.
In addition, we will end with a hands-on session where you can try out
Julia and Trixi.jl for yourself using these notebooks.

**Note:** The tutorial is intended for researchers who are already
familiar with at least one other high-level language scientific programming
language such as Python, C/C++, or Fortran.


## Getting started

You can view a static version of the Jupyter notebooks `*.ipynb`

- directly on GitHub (select the notebook; this may fail sometimes)
- or on [nbviewer.jupyter.org](https://nbviewer.jupyter.org/)
  (select the "render" badges in the table of contents above)

These static versions do not contain output of the code cells.

Below you will find information on how to use the notebooks either via
[mybinder.org](#using-mybinderorg) or by
[setting up a local installation](#setting-up-a-local-juliajupyter-installation).
As an alternative to using Jupyter, you may also just copy the code from the
notebooks into the [Julia REPL](#using-the-julia-repl) and execute it there.

*General note:* Make sure that you execute the examples (either in the notebook
or in the REPL) *in order*, at least for the first time. Both the notebook and
the Julia REPL maintain an internal state and and some snippets depend on
earlier statements having been executed.

### Using mybinder.org
The easiest way to get started is to click on the *Launch Binder* badges
in the table of contents above.
This launches the notebook for interactive use in your browser without the need
to download or install anything locally.

In this case, you can skip the rest of this *Getting started* section. A
Jupyter instance will be started automagically in the cloud via
[mybinder.org](https://mybinder.org), and the notebook will loaded directly from
this repository.

*Note:*  Depending on current usage and available resources, it typically takes
a few minutes to launch a notebook with [mybinder.org](https://mybinder.org)
(sometimes a little longer), so try to remain patient. Similarly, the first two
cells of the notebook take much longer to execute than usual (around 1.5 minutes
for the first Trixi.jl simulation and about 1 minute for the first plot), since
Julia compiles all methods "just-ahead-of-time" at first use. Subsequent runs
will be much faster.

### Setting up a local Julia/Jupyter installation
Alternatively, you can also clone this repository and open the notebook on your
local machine. This is recommended if you already have a Julia + Jupyter setup
or if you plan to try out Julia anyways.

#### Installing Julia and IJulia
To obtain Julia, go to https://julialang.org/downloads/ and download the latest
stable release (v1.8.5 as of 2023-01-15; neither use the LTS release nor
Julia Pro!). Then, follow the
[platform-specific instructions](https://julialang.org/downloads/platform/)
to install Julia on your machine. Note that there is no need to compile anything
if you are using Linux, MacOS, or Windows.

After the installation, open a terminal and start the Julia *REPL*
(i.e., the interactive prompt) with
```shell
julia
```
To use the notebook, you also need to get the
[IJulia](https://github.com/JuliaLang/IJulia.jl) package, which provides a Julia
backend for Jupyter. In the REPL, execute
```julia
using Pkg
Pkg.add("IJulia")
```
to install IJulia. For more details, especially on how to use an existing Jupyter
installation, please refer to the
[IJulia documentation](https://julialang.github.io/IJulia.jl/stable/).
From here on, we assume that you have a working installation of Julia, Jupyter,
and the Julia kernel for Jupyter.

#### Installing the required Julia packages
To make the notebook fully reproducible, we have used Julia's package manager
to pin all packages to a fixed release. This ensures that you always have a
Julia environment in which all examples in this notebook work. Later you can
always install the latest versions of Trixi.jl and its dependencies by following
the instructions in the Trixi
[documentation](https://trixi-framework.github.io/Trixi.jl/stable/).

If you have not done it yet, clone the repository where this notebook is stored:
```shell
git clone https://github.com/trixi-framework/tutorial-2023-snubic.git
```
Then, navigate to your repository folder and install the required packages:
```shell
cd tutorial-2023-snubic
julia --project=. -e 'using Pkg; Pkg.instantiate()'
```
This will download and build all required packages, including the ODE package
[OrdinaryDiffEq](https://github.com/SciML/OrdinaryDiffEq.jl), the visualization
package [Plots](https://github.com/JuliaPlots/Plots.jl), and of course
[Trixi.jl](https://github.com/trixi-framework/Trixi.jl).
The `--project=.` argument tells Julia's package manager
[Pkg.jl](https://pkgdocs.julialang.org/v1/)
to use the [`Project.toml`](Project.toml) and [`Manifest.toml`](Manifest.toml)
files from this repository to figure out which packages to install.

#### Starting JupyterHub from Julia
You can finally start JupyterHub from Julia using the following command inside
the repository folder:
```shell
julia -e 'using IJulia; jupyterlab(dir=".")'
```

### Using the Julia REPL
If you want, you can also directly execute the notebook contents in the Julia
REPL. In this case, please also follow the instructions on installing the
required Julia packages [above](#installing-the-required-julia-packages). Then,
start the REPL inside the repository folder with
```shell
julia --project=.
```


## Authors
This repository was created by [Michael
Schlottke-Lakemper](https://lakemper.eu). It is based on a tutorial previously
given at [ICOSAHOM 2021](https://github.com/trixi-framework/tutorial-2021-icosahom),
which was initiated jointly by [Hendrik Ranocha](https://ranocha.de), Michael
and [Andrew R. Winters](https://liu.se/en/employee/andwi94).


## License
The contents of this repository are licensed under the MIT license
(see [LICENSE.md](LICENSE.md)).
