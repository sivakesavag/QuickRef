# Chapter 26: Data Visualization

**Target MCQs**: 50-60
**Current Batch**: 1-30
**Topics Covered**: `matplotlib` basics (Figures, Axes, Subplots), Line/Bar/Scatter/Hist/Pie plots, `searborn` styles, Distplots, Heatmaps, Boxplots, Saving figures, `plotly` basics (interactive).

---

**Q26.1: Basic - [Matplotlib Default API]**

The most common way to import individual plotting functions from Matplotlib is:

A) `import matplotlib.pyplot as plt`
B) `import matplotlib as mpl`
C) `import pyplot`
D) `import plt`

**Answer: A**

**Explanation:**
The `pyplot` state-machine interface mimicks MATLAB.

---

**Q26.2: Intermediate - [Figure vs Axes]**

In the Object-Oriented interface (`fig, ax = plt.subplots()`), the `Figure` represents:

A) The axes only.
B) The entire container/window holding all plots, titles, and legends.
C) A single line.
D) The X-axis.

**Answer: B**

**Explanation:**
`Axes` represents an individual plot (with x/y axis). A Figure can contain multiple Axes.

---

**Q26.3: Advanced - [Seaborn Distplot]**

`sns.histplot(data=df, x='col', kde=True)` displays:

A) A histogram with an overlaid Kernel Density Estimate (KDE) line (smooth probability distribution).
B) A pie chart.
C) A scatter plot.
D) A 3D map.

**Answer: A**

**Explanation:**
Standard way to visualize the distribution of a univariable.

---

**Q26.4: Basic - [Bar Chart]**

To create a vertical Bar Chart:

A) `plt.bar(x, height)`
B) `plt.plot(x, y)`
C) `plt.scatter(x, y)`
D) `plt.pie(x)`

**Answer: A**

**Explanation:**
`barh` for horizontal bars.

---

**Q26.5: Intermediate - [Save Figure]**

To save a plot to a PNG file with high resolution:

A) `plt.save('plot.png')`
B) `plt.savefig('plot.png', dpi=300)`
C) `plt.export('plot.png')`
D) `plt.write('plot.png')`

**Answer: B**

**Explanation:**
`dpi` (dots per inch) controls quality. `bbox_inches='tight'` helps prevent cutting off labels.

---

**Q26.6: Advanced - [Subplots]**

`plt.subplots(nrows=2, ncols=2)` returns:

A) A Figure and a 2x2 NumPy array of Axes objects.
B) 2 plots.
C) 4 Figures.
D) An error.

**Answer: A**

**Explanation:**
Allows accessing individual subplots via `axes[0,0]`, `axes[0,1]`, etc.

---

**Q26.7: Expert - [Twin Axes]**

`ax2 = ax1.twinx()` creates:

A) A duplicate plot.
B) A second Axes that shares the same x-axis but has a separate (independent) y-axis (useful for plotting two datasets with different scales on the same chart).
C) A clone of the object.
D) A mirror image.

**Answer: B**

**Explanation:**
Common visualization technique (e.g., Temp vs Rain on same timeline).

---

**Q26.8: Basic - [Grid]**

To turn on the grid lines:

A) `plt.grid(True)`
B) `plt.line()`
C) `plt.show_grid()`
D) `plt.net()`

**Answer: A**

**Explanation:**
Helps reading values.

---

**Q26.9: Intermediate - [Box Plot]**

A Box Plot (`plt.boxplot` or `sns.boxplot`) visually summarizes:

A) All data points.
B) Five-number summary: Minimum, First Quartile (Q1), Median, Third Quartile (Q3), Maximum, and potential outliers.
C) The average only.
D) A box.

**Answer: B**

**Explanation:**
Excellent for comparing distributions and spotting outliers across categories.

---

**Q26.10: Advanced - [Seaborn Styles]**

`sns.set_style("whitegrid")`:

A) Changes the global default matplotlib aesthetics to the Seaborn "whitegrid" theme.
B) Draws a grid.
C) Deletes the styling.
D) Is invalid.

**Answer: A**

**Explanation:**
Seaborn makes Matplotlib look better by default.

---

**Q26.11: Basic - [Pie Chart]**

Pie charts are generally discouraged in data science because:

A) They are hungry.
B) Validating angles/areas is harder for the human eye than comparing bar lengths.
C) Python cannot draw circles.
D) They are black and white.

**Answer: B**

**Explanation:**
Bar charts are usually preferred for comparing categorical precision.

---

**Q26.12: Intermediate - [Heatmap]**

`sns.heatmap(df.corr(), annot=True)` is widely used to:

A) Visualize the correlation matrix with color intensity representing correlation strength.
B) Show weather.
C) Draw a map.
D) Plot a line.

**Answer: A**

**Explanation:**
`annot=True` writes the numerical values in the cells.

---

**Q26.13: Advanced - [Plotly Interactive]**

The main advantage of Plotly (`plotly.express`) over separate image files from Matplotlib is:

A) It works offline.
B) It generates interactive HTML/JS plots (allowing zoom, pan, hover tooltips) embedded in the browser/notebook.
C) It is older.
D) It is black and white.

**Answer: B**

**Explanation:**
Essential for dashboards and exploring dense data points.

---

**Q26.14: Expert - [Hue Semantic]**

In Seaborn, passing `hue='category_column'` to a plot (e.g., scatterplot) will:

A) Color the points based on the values in 'category_column', automatically adding a legend.
B) Change the background color.
C) Do nothing.
D) Error.

**Answer: A**

**Explanation:**
Maps a variable to color (multivariate analysis).

---

**Q26.15: Intermediate - [Tight Layout]**

`plt.tight_layout()` helps to:

A) Squeeze the plot.
B) Automatically adjust subplot parameters to give specified padding, fixing overlapping labels/titles.
C) Make lines tighter.
D) Close the window.

**Answer: B**

**Explanation:**
Almost always necessary when using subplots.

---

**Q26.16: Basic - [Xlabel]**

To adds a label to the X-axis:

A) `plt.xlabel('My Label')`
B) `plt.x('My Label')`
C) `plt.label('x', 'My Label')`
D) `plt.text('My Label')`

**Answer: A**

**Explanation:**
And `plt.ylabel()` for Y.

---

**Q26.17: Advanced - [Violin Plot]**

A Violin Plot (`sns.violinplot`) combines:

A) A violin and a piano.
B) A Box Plot and a Kernel Density Estimation (KDE), showing different shapes of distribution (e.g. bimodal).
C) A line and bar.
D) Sound.

**Answer: B**

**Explanation:**
More informative than a boxplot because it shows the probability density at different values.

---

**Q26.18: Intermediate - [Pairplot]**

`sns.pairplot(df)` generates:

A) A grid of scatterplots for every pair of numeric variables in the dataframe.
B) Two plots.
C) A pair of shoes.
D) A single scatter plot.

**Answer: A**

**Explanation:**
Quick way to see relationships across the entire dataset during EDA.

---

**Q26.19: Basic - [Legend]**

`plt.legend()` displays:

A) A story.
B) The labels defined in plot commands (e.g., `label="Line A"`) in a box key.
C) The title.
D) The axis values.

**Answer: B**

**Explanation:**
Identifies which line/color corresponds to which data series.

---

**Q26.20: Expert - [3D Plots]**

Matplotlib supports 3D plotting via:

A) `from mpl_toolkits.mplot3d import Axes3D`.
B) It does not support 3D.
C) `plt.plot3d()`.
D) Default.

**Answer: A**

**Explanation:**
Adds the `projection='3d'` capability to axes.

---

**Q26.21: Intermediate - [Log Scale]**

`plt.yscale('log')` is useful when:

A) Creating logs.
B) Data spans several orders of magnitude (e.g., 10, 1000, 1000000), allowing small variations to be seen alongside large ones.
C) Plotting trees.
D) Data is negative.

**Answer: B**

**Explanation:**
Compresses the axis. Common in financial or scientific plots.

---

**Q26.22: Basic - [Scatter Marker]**

To change the point style in scatter to 'X':

A) `marker='x'`
B) `style='x'`
C) `point='x'`
D) `shape='x'`

**Answer: A**

**Explanation:**
Standard markers: 'o', 'x', '+', '.', etc.

---

**Q26.23: Advanced - [Color Map]**

A "colormap" (`cmap='viridis'`) maps:

A) Values to Colors.
B) Colors by name.
C) Maps to locations.
D) Nothing.

**Answer: A**

**Explanation:**
Important to choose perceptually uniform colormaps (like 'viridis') rather than 'jet'.

---

**Q26.24: Expert - [Interactive Notebook]**

`%matplotlib inline` in Jupyter:

A) Draws plots inline in the notebook (static images).
B) Makes python faster.
C) Is required for loops.
D) Opens a window.

**Answer: A**

**Explanation:**
Though mostly default now, historically required. `%matplotlib widget` (ipympl) enables interactivity.

---

**Q26.25: Intermediate - [Countplot]**

`sns.countplot(x='cat_col')` is roughly equivalent to:

A) `df['cat_col'].value_counts().plot(kind='bar')`.
B) A histogram.
C) `plt.count()`.
D) A pie chart.

**Answer: A**

**Explanation:**
Ideally suited for categorical counts.

---

**Q26.26: Basic - [Title]**

To set the plot title:

A) `plt.title("My Plot")`
B) `plt.name("My Plot")`
C) `plt.header("My Plot")`
D) `plt.text("My Plot")`

**Answer: A**

**Explanation:**
Top of the chart.

---

**Q26.27: Advanced - [Alpha Channel]**

Setting `alpha=0.5` in a plot command:

A) Sets the line width.
B) Sets the transparency/opacity (0.0 transparent to 1.0 opaque).
C) Sets the color to red.
D) Sorts the data.

**Answer: B**

**Explanation:**
Useful when plotting many overlapping points or lines.

---

**Q26.28: Expert - [FacetGrid]**

`sns.FacetGrid(df, col='category').map(plt.hist, 'value')`:

A) Creates a grid of histograms, one for each unique value in 'category'.
B) Draws a face.
C) Maps locations.
D) Is slow.

**Answer: A**

**Explanation:**
Powerful "Small Multiples" technique for comparing conditional distributions.

---

**Q26.29: Intermediate - [Error Bars]**

`plt.errorbar(x, y, yerr=errors)`:

A) Plots points with lines indicating the uncertainty/margin of error.
B) Plots mistakes.
C) Deletes errors.
D) Plots bars.

**Answer: A**

**Explanation:**
Scientific standard for showing variability.

---

**Q26.30: Basic - [Line Style]**

To make a dashed line:

A) `linestyle='--'`
B) `line='dashed'`
C) `style='dash'`
D) `dash=True`

**Answer: A**

**Explanation:**
Also `':'` (dotted), `'-.'` (dash-dot).

---

**Q26.31: Intermediate - [Annotate]**

`plt.annotate('Text', xy=(2, 5), xytext=(3, 6), arrowprops=dict(facecolor='black'))`:

A) Draws an arrow pointing to `(2, 5)` with text at `(3, 6)`.
B) Draws a circle.
C) Writes text only.
D) Errors.

**Answer: A**

**Explanation:**
Great for highlighting specific data points (e.g., "Peak sales").

---

**Q26.32: Advanced - [Seaborn Context]**

`sns.set_context("talk")`:

A) Scales plot elements (fonts, lines) to be larger and more readable for a presentation/talk.
B) Enables audio.
C) Resets the context.
D) Makes plot smaller (for "paper").

**Answer: A**

**Explanation:**
Options: `paper` (default), `notebook`, `talk`, `poster`.

---

**Q26.33: Basic - [Rotate Ticks]**

If X-axis labels are overlapping, commonly used fix is:

A) `plt.xticks(rotation=45)`
B) `plt.rotate()`
C) `plt.flip()`
D) `plt.clear()`

**Answer: A**

**Explanation:**
Rotates the text labels.

---

**Q26.34: Expert - [Artist Layer]**

Matplotlib has three layers: Backend, Artist, and Scripting. The "Artist" layer handles:

A) Everything you see on the figure (lines, text, axis region).
B) The window.
C) `plt.plot()` commands only.
D) Saving files.

**Answer: A**

**Explanation:**
`Axes`, `Line2D`, `Text` are all Artists.

---

**Q26.35: Intermediate - [JointPlot]**

`sns.jointplot(x='x', y='y', data=df)`:

A) Draws a scatter plot in the center and marginal histograms/density plots on the top and right axes.
B) Joins two dataframes.
C) Plots a line.
D) Is deprecated.

**Answer: A**

**Explanation:**
Visualises bivariate relationship and univariate distributions simultaneously.

---

**Q26.36: Advanced - [Plotly Graph Objects]**

Compared to `plotly.express` (px), `plotly.graph_objects` (go) is:

A) More low-level, allowing finer control over every detail of the figure construction.
B) Faster.
C) For 3D only.
D) Deprecated.

**Answer: A**

**Explanation:**
`px` is high-level wrapper; `go` gives you the raw dictionary-like building blocks (`go.Scatter`, `go.Figure`).

---

**Q26.37: Basic - [Plot]**

`plt.plot([1, 2, 3])` assumes the X-axis values are:

A) `[0, 1, 2]` (Indices).
B) `[1, 2, 3]`.
C) Random.
D) Empty.

**Answer: A**

**Explanation:**
If only one array is passed, matplotlib assumes it's the Y-values and uses the index for X.

---

**Q26.38: Intermediate - [Cmap Reverse]**

To reverse a colormap (e.g., 'viridis'), typically append:

A) `_r` (e.g., `cmap='viridis_r'`).
B) `_reverse`.
C) `-1`.
D) `(reverse=True)`.

**Answer: A**

**Explanation:**
Standard convention in matplotlib.

---

**Q26.39: Advanced - [Despine]**

`sns.despine()` removes:

A) The top and right spines (borders) of the plot by default.
B) The x-axis.
C) The grid.
D) The labels.

**Answer: A**

**Explanation:**
Cleaner "Tufte-style" look (maximizing data-ink ratio).

---

**Q26.40: Expert - [Imshow]**

`plt.imshow(img_array)` is primarily used for:

A) Displaying image data (2D/3D arrays of pixels).
B) Showing a line chart.
C) Opening a file dialog.
D) Internet browsing.

**Answer: A**

**Explanation:**
Origin is usually at the top-left for images, unlike standard plots (bottom-left).

---

**Q26.41: Basic - [Ylim]**

To set the limits of the Y-axis:

A) `plt.ylim(0, 100)`
B) `plt.limit(y=[0, 100])`
C) `plt.range(0, 100)`
D) `plt.ymax(100)`

**Answer: A**

**Explanation:**
Zooms into a specific range.

---

**Q26.42: Intermediate - [Stacked Bar]**

To create a stacked bar chart with `plt.bar`:

A) Use the `bottom` parameter (e.g., `plt.bar(x, y2, bottom=y1)`).
B) Use `stacked=True`.
C) Use `plt.stack()`.
D) It's impossible.

**Answer: A**

**Explanation:**
This lifts the second set of bars to start where the first set ends.

---

**Q26.43: Advanced - [Swarm Plot]**

`sns.swarmplot()` is similar to a strip plot but:

A) Adjusts the points along the categorical axis so they don't overlap (beeswarm).
B) Randomly scatters them.
C) Connects them.
D) Hides them.

**Answer: A**

**Explanation:**
Great for small datasets to show every observation without obfuscation.

---

**Q26.44: Expert - [FuncAnimation]**

`matplotlib.animation.FuncAnimation` is used to:

A) Create animations by repeatedly calling a function that updates the plot data.
B) Play a video file.
C) Animate the window opening.
D) Gif conversion.

**Answer: A**

**Explanation:**
Can export to .mp4 or .gif.

---

**Q26.45: Intermediate - [Style Sheets]**

`plt.style.use('ggplot')` mimics the aesthetic of:

A) The R library `ggplot2`.
B) Google Plots.
C) Green Plots.
D) Graph Plot.

**Answer: A**

**Explanation:**
Famous for its gray background and white gridlines.

---

**Q26.46: Basic - [Semicolon Trick]**

Putting a semicolon `;` at the end of the last plotting command in a Jupyter cell:

A) Suppresses the text output (e.g., `<matplotlib.axes...>`) and shows only the plot.
B) Errors.
C) Saves the plot.
D) Is mandatory.

**Answer: A**

**Explanation:**
Cleaner notebook output.

---

**Q26.47: Advanced - [KDE Plot]**

A KDE (Kernel Density Estimate) plot represents:

A) A smooth estimate of the probability density function (PDF).
B) A cumulative sum.
C) A discrete count.
D) A scatter.

**Answer: A**

**Explanation:**
Continuous alternatve to a histogram.

---

**Q26.48: Expert - [RcParams]**

`plt.rcParams['figure.figsize'] = (10, 6)`:

A) Globally updates the default figure size for all subsequent plots.
B) Changes only the current plot.
C) Is invalid syntax.
D) Reinstalls matplotlib.

**Answer: A**

**Explanation:**
Runtime Configuration Parameters (`rcParams`) control defaults (fonts, colors, sizes) dynamically.

---

**Q26.49: Intermediate - [Hexbin]**

`plt.hexbin(x, y)` is a good alternative to scatter plots when:

A) You have millions of points (overplotting), and it bins them into hexagons shaded by density.
B) You like shapes.
C) You have 6 points.
D) Data is categorical.

**Answer: A**

**Explanation:**
Efficient for visualizing density in large datasets.

---

**Q26.50: Basic - [Savefig Transparent]**

`plt.savefig('logo.png', transparent=True)`:

A) Saves the plot with a transparent background.
B) Saves an invisible file.
C) Errors.
D) Makes the lines transparent.

**Answer: A**

**Explanation:**
Useful for integrating plots into slides or websites.

---

---

## Review Notes (2026-02-06)

- No major content errors were identified in this review pass.
