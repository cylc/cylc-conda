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

## References:

- https://github.com/bioconda/bioconda-recipes/tree/master/recipes
- https://medium.com/@giswqs/building-a-conda-package-and-uploading-it-to-anaconda-cloud-6a3abd1c5c52
- https://docs.conda.io/projects/conda-build/en/latest/resources/define-metadata.html