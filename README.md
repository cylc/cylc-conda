# Cylc Conda

Conda recipe for Cylc 8.

e.g.

```
cd recipes
conda skeleton pypi isodatetime
conda build isodatetime
anaconda login
anaconda upload ~/Development/python/anaconda3/conda-bld/linux-x86/isodatetime*.tar.bz2
conda build purge 
```

Example `.condarc`:

```
channels:
  - defaults
  - conda-forge
  - kinow
ssl_verify: true
auto_activate_base: false
anaconda_upload: false
```

If not loading Anaconda by default, due to issue #7980, you will need to source something similar to:

```
#!/bin/bash

PATH=~/Development/python/anaconda3/bin:$PATH
. ~/Development/python/anaconda3/etc/profile.d/conda.sh
```

The work directory of a conda environment can be accessed via an environment variable, allowing us thus
to build up the Cylc UI directory as follows: `${CONDA_PREFIX}/work/cylc-ui`.

## Testing

You need to enable the `kinow` channel for this test to work (see `.condarc` file above).

Then create a new Conda environment, e.g. `cylc1`.

- `conda create -n cylc1`
- `conda activate cylc1`

Now you only need to install the placeholder package "cylc". You can refer to the `.recipes/cylc/meta.yaml`
for its contents. But this is basically installing conda packages for `metomi-isodatetime`, `cylc-flow`,
`cylc-uiserver`, and unzipping `cylc-ui` into the conda environment work directory (`$PREFIX` conda build env
var).

- `conda install cylc` (you can wait for the confirmation question, where you have a chance to see all the packages being installed, including a few cylc* and metomi*)

At this point you can test your environment if you would like, with some commands like:

- `cylc --version`
- `cylc run --no-detach five` (or any other suite you use for testing)
- `cylc-uiserver --help`
- `isodatetime`

Finally, if you found nothing wrong with your environment, start the hub with:

- `jupyterhub --JupyterHub.spawner_class="jupyterhub.spawner.LocalProcessSpawner" --Spawner.args="['-s', '${CONDA_PREFIX}/work/cylc-ui']" --Spawner.cmd="cylc-uiserver" --JupyterHub.logo_file="${CONDA_PREFIX}/work/cylc-ui/img/logo.png"`

Voilà 🎉. Go to `http://localhost:8000`, log in with your local user credentials, and enjoy Cylc 8 alpha!

You can now remove the environment if you would like.

- `conda deactivate`
- `conda env remove -n cylc1`

_ps: we could use the `jupyterhub_config.py` shipped with cylc-uiserver, but that file is not included in
the wheel file, so conda install cylc-uiserver does not downloads it. We could still download from GitHub,
but that would be over-complicating for this quick experiment IMHO._

## References:

- https://github.com/bioconda/bioconda-recipes/tree/master/recipes
- https://medium.com/@giswqs/building-a-conda-package-and-uploading-it-to-anaconda-cloud-6a3abd1c5c52
- https://docs.conda.io/projects/conda-build/en/latest/resources/define-metadata.html
