# About the _brat_ directory

These files and folders should be placed in brat's ```data/``` directory.

```Hill.txt``` and ```Nonverbs.txt``` are normalization files that need to be converted to normalization databases. To do so, follow the [brat normalization](https://brat.nlplab.org/normalization.html) instructions. In particular, something like the following command should be run for each file:

```python tools/norm_db_init.py data/Hill.txt```
