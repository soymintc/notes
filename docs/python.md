# Python
Personal cheatsheet

## Reset matplotlib font
1. Download font ttf files (e.g. Arial.ttf)
2. Remove the gaddamn matplotlib cache
```bash
mpl_cache_dir=~/chois7/.cache/matplotlib
[ -d $mpl_cache_dir ] && { echo "$mpl_cache_dir exists - removing it"; rm -rf $mpl_cache_dir; }
```
3. Plug in the font using matplotlib fontmanager
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
