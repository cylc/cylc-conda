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