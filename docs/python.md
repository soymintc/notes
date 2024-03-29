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
1. Go to your `$VENV/lib`
2. Remove `libstdc++.so` and `libstdc++.so.6` if linked to `libstdc++.so.6.0.21`, replace with `libstdc++.so.6.0.32`

