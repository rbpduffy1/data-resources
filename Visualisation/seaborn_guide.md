# Seaborn guide
All Seaborn functions follow some basic rules. 

* We need our variable, `x`.
* We need the `data` parameter. 
* If we want, we also *could* add a grouping variable by adding a `hue` parameter.
* Some graphs require two variables at least, and so will also need a `y` parameter. 

Below is a quick guide to how Seaborn functions work. *Note that this is not a comprehensive list of all seaborn functions! There are many more.*

|No. of variables|Data type(s)|Graph type(s)|Seaborn function|Necessary parameters|Interesting optional parameters |
| --- | --- | --- | --- | --- | --- |
| One | Numerical | Distribution plot/Histogram | sns.distplot() | `a`; <br>`data` | `hue`; <br> `kde`; <br> `bins`; |
| One | Categorical | Count plot | sns.countplot() | `x`; <br>`data` | `hue`; <br> `kde`; <br> `bins`; |
| One | Numerical | Distribution plot/Histogram | sns.distplot() | `a`; `data` | `hue`; <br> `kde`; <br> `bins`; |
| One | Numerical | Distribution plot/Histogram | sns.distplot() | `a`; `data` | `hue`; <br> `kde`; <br> `bins`; |

