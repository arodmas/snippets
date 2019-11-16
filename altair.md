# Import altair

# Chart types

```python
import altair as alt

#if in notebook
alt.renderers.enable("notebook")
```

# Histograma

```python
alt.Chart(df).mark_bar().encode(
    x=alt.X('Brain Weight', bin=alt.Bin(maxbins=20)),title="Brain Weight Binned",
    y='count()'
).properties(
    width=200,
    height=200,
    title='Histogram of Brain Weight'
    )
```

# Scatter Plot

```python
scatter = alt.Chart(df).mark_circle().encode(
    x="Body Weight",
    y="Brain Weight"
)
```

# Bar Chart

```python
trends_bar = alt.Chart(trends).mark_bar().encode(
    x="search_term",
    y="sum(value)",
    color="search_term"
).transform_filter(
    select_interval
)    
```

# Line Chart
```

trends_line = alt.Chart(trends).mark_line().encode(
    x=alt.X("date:T",timeUnit="yearmonth"),
    y="sum(value)",
    color="search_term"
).properties(
    selection=select_interval
)
```
# Map
# Horizontal concatenation
```python
trends_bar|trends_line
```

# Vertical concatenation
```python
trends_bar&trends_line
```

# Interactives
# Single selection
```python
select_interval = alt.selection_interval(encodings=["x"])

trends_line = alt.Chart(trends).mark_line().encode(
    x=alt.X("date:T",timeUnit="yearmonth"),
    y="sum(value)",
    color="search_term"
).properties(
    selection=select_interval
)

trends_bar = alt.Chart(trends).mark_bar().encode(
    x="search_term",
    y="sum(value)",
    color="search_term"
).transform_filter(
    select_interval
)    

(trends_bar|trends_line)
```

# Interval Selection
```python
# zoom
selection2 = alt.selection_interval(encodings=["x"])

trends_line_nozoom = alt.Chart(trends).mark_line().encode(
    x=alt.X("date:T",timeUnit="yearmonth"),
    y="sum(value)",
    color="search_term"
).transform_filter(
    selection2
)

trends_line_small = alt.Chart(trends).mark_line().encode(
    x=alt.X("date:T",timeUnit="yearmonth"),
    y="sum(value)",
    color="search_term"
).properties(
        height=50,
        selection=selection2,
        title='Histogram of Brain Weight'
)

(trends_line_nozoom&trends_line_small)
```
