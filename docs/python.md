# Python
Personal cheatsheet

## Reset matplotlib font
1. Download font ttf files (e.g. Arial.ttf)
2. Remove the gaddamn matplotlib cache
```bash
mpl_cache_dir=~/chois7/.cache/matplotlib
[ -d $mpl_cache_dir ] && { echo "$mpl_cache_dir exists - removing it"; rm -rf $mpl_cache_dir; }
```
3. Run `fc-cache` in the directory you have .ttf files in, and then `fc-list` to check
4. Plug in the font using matplotlib fontmanager
```python
import matplotlib.font_manager as font_manager
arial_path = "/path/to/Arial.ttf"
arial_italic_path = "/path/to/Arial-Italic.ttf"
arial = font_manager.FontProperties(fname=arial_path)
arial_italic = font_manager.FontProperties(fname=arial_italic_path)
plt.rcParams['font.family'] = fontprop.get_name()
with matplotlib.rc_context({'font.family':'Arial', 'font.size': 15}):
    # plots, plots, and plots
    # whenever necessary shove in `fontproperties=fontprop` into a function
```

## Easy way of appending a row to a DataFrame
```python
df = pd.DataFrame(columns=['A', 'B', 'count'])
for ix, val in enumerate(some_data):
    A = some_data.do_something()
    B = some_data.do_something_else()
    count = count_dict[(A, B)]
    df.loc[ix] = [A, B, count] # best to use loc here
```

## Run `bash` script in python foreground
```python
subprocess.run(["ls", "-l"]) # no output capture
subprocess.run("ls -l", shell=True) # using shell argument
subprocess.run(["ls", "-l", "/dev/null"], capture_output=True) # capture stdout
```
```python
# subprocess.run 
subprocess.run(args, *, stdin=None, input=None, stdout=None, stderr=None, capture_output=False, shell=False, cwd=None, timeout=None, check=False, encoding=None, errors=None, text=None, env=None, universal_newlines=None, **other_popen_kwargs)
```

## Easy build and upload to `pypi` after writing setup.py
```bash
python setup.py sdist bdist_wheel
pytest # if test files written
twine upload dist/*
````

## Find value changes in a pandas DataFrame
```python
cn["state_change"] = (cn["state"].shift(1, fill_value=cn["state"].head(1).squeeze()) != cn["state"])
```

## Adding two separate custom legends to pyplot Axes
```python
handle1 = [plt.plot([], [], 
           color=colors[label], marker="o", ms=4, ls="")[0] for label in colors]
legend1 = ax.legend(handles=handle1, labels=colors.keys(), title="Color labels")
ax.add_artist(legend1);
handle2 = [plt.plot([], [], 
           color="gray", marker="o", ms=2, ls="")[0]]
legend2 = ax.legend(handles=handle2, labels=[''], title="Background", loc=(0.823,0.50))
ax.add_artist(legend2);
```

## How to fix pd.DataFrame.groupby row duplication bugs
```python
df = df.drop_duplicates()
df = df.reset_index(drop=True)
df[index_cols] = df[index_cols].astype(str) # or category
# only then do a groupby operation
```

## Change pyplot background colors
Usually I want the figure and savefig facecolor to be (1.0, 1.0, 1.0, 1.0)
```python
plt.rcParams.update({
    "axes.facecolor":    (0.0, 1.0, 0.0, 0.5),  # figure main background color
    "figure.facecolor":  (1.0, 0.0, 0.0, 0.3),  # applied for .show()
    "savefig.facecolor": (0.0, 0.0, 1.0, 0.2),  # applied for .savefig()
})
```

## Sphinx-compatible function docstrings
```python
"""[Summary]

:param [ParamName]: [ParamDescription], defaults to [DefaultParamVal]
:type [ParamName]: [ParamType](, optional)
...
:raises [ErrorType]: [ErrorDescription]
...
:return: [ReturnDescription]
:rtype: [ReturnType]
"""
```

## `tqdm` for pandas
```python
for ix, row in tqdm(df.iterrows(), total=df.shape[0]):
    # do something
```

## Fix `libstdc++.so.6: version 'GLIBCXX_3.4.29' not found` issue
You could type in the following in your shell, or add into your rc file:
```bash
find /path/to/your/env -name libstdc++.so.6`
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/path/to/your/env/lib
```

## Set argparse bool flag
The following allows a flag to be set to `True` only when the flag is used
```python
p.add_argument('--flag', help='bool flag', default=False, action='store_true')
```

## Relative imports for `pytest`
1. Make sure `pytest` has been installed in your environment. Else a `pytest` binary installed in some other weird or default environment can screw things up, e.g. giving `ModuleNotFound` errors.
2. Say under the project root directory, there are `src/` and  `tests/` directories, and `tests/test_something.py` imports something from `src/`. Then add `__init__.py` to all the directories.
3. From `tests/test_something.py`, import a package in `src/` as follows `from src.something import module_to_test`

## `read_csv` from Google spreadsheets
By far the following is the best way to open public spreadsheets
```python
sheet_id = "1ckIGloNHblgtfNyzC65TenCzcKxIMAw4C5xbzAIzio4"
gid = '1256376105'
url = f"https://docs.google.com/spreadsheets/d/{sheet_id}/gviz/tq?tqx=out:csv&gid={gid}"
df = pd.read_csv(url, on_bad_lines='warn')
```

## Some notes about `click`
- Structure
```python
@click.command()
@click.option('-i', '--input', required=True, help="input file")
def some_function(input):
    foo = 1
    bar = process_arg(foo)
    return bar
if __name__ == "__main__":
    some_function()
```
- Option for multiple inputs
To be used as `python script.py --bam 1.bam --bam 2.bam`
```python
@click.option('--bam', multiple=True, help="input tumor bam path(s)")
```
- Option for setting types and default values
```python
@click.option('--cutoff', type=int, default=1, help="support cutoff")
```
- Option used as flag
```python
@click.option('--verbose', '-v', is_flag=True, help="print more output")
```

## Customize pylint
Generate a pylint rc file, then edit e.g. disable part to remove `E\d{4}` errors
```bash
pylint --generate-rcfile > ~/.pylintrc
```

## Packaging
Bare bones of packaging a project, but still basing on 2024 standards.
1. Generate a `pyproject.toml`, e.g. https://github.com/shahcompbio/ontmont/blob/main/pyproject.toml
2. Make a requirements file from the source directory. I found `pipreqs . > requirements.txt` pleasing to use
3. Add a shim `setup.py` for `setuptools`, e.g. https://github.com/shahcompbio/ontmont/blob/main/setup.py
4. Build into dist: `python -m build`. Remember to check your project version before doing this
5. Test publishing to TestPyPI: `twine upload --repository testpypi dist/*`. Before doing this and the PyPI publishing below, make sure to have your API tokens saved in your PyPI rc file, e.g. `~/.pypirc`. You also don't want your files to be read by others, so `chmod 600 ~/.pypirc` before anything
6. If feeling lucky, publish to PyPI: `twine upload --repository pypi dist/*`

## ReadTheDocs setup with `sphinx`
- The backbone of setups are in https://sphinx-rtd-tutorial.readthedocs.io/en/latest/build-the-docs.html
- Some changes that I learned the hard way:
    1. `requirements.txt` should contain all the packages used in the modules + read the docs-related packages
        ```bash
        $ cat requirements.txt
        click
        matplotlib
        numpy
        pandas
        pydata-sphinx-theme
        pyfaidx
        pysam
        pytest
        PyYAML
        scipy
        setuptools
        sphinxcontrib-napoleon
        swalign
        tqdm
        ```
    2. Make sure `.readthedocs.yaml` at the project root points to the `requirements.txt` file
    3. Set up custom settings in `docs/conf.py`, e.g. following napoleon settings: https://www.sphinx-doc.org/en/master/usage/extensions/napoleon.html
    4. The `sys.path.insert(0, os.path.abspath('../'))` line in `docs/conf.py` should point to the parent directory of the target module for documentation
