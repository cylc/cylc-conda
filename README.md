# Cylc Conda

Conda recipe for Cylc 8.

e.g.

```
cd recipes
conda build skeleton pypi isodatetime
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

## References:

- https://github.com/bioconda/bioconda-recipes/tree/master/recipes
- https://medium.com/@giswqs/building-a-conda-package-and-uploading-it-to-anaconda-cloud-6a3abd1c5c52
- https://docs.conda.io/projects/conda-build/en/latest/resources/define-metadata.html
