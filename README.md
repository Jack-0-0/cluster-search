cluster-search
================

## Install

You can install via pip with the following command:

`pip install cluster-search`

## Documentation

Documentation can be found [here](https://jack-0-0.github.io/cluster-search/)
PyPI site can be found [here](https://pypi.org/project/cluster-search/)

## An example on how to use

Below is an example of using
the `grid_search` function
to perform grid search over some clustering models and model parameters
to find the highest silhouette score when clustering a sample of the
iris dataset:

``` python
from sklearn import datasets
from cluster_search.cluster_grid_search import cluster, grid_search
```

``` python
from sklearn import datasets
iris = datasets.load_iris(as_frame=True)
X = iris.data
X.head(5)
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>sepal length (cm)</th>
      <th>sepal width (cm)</th>
      <th>petal length (cm)</th>
      <th>petal width (cm)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>5.1</td>
      <td>3.5</td>
      <td>1.4</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4.9</td>
      <td>3.0</td>
      <td>1.4</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4.7</td>
      <td>3.2</td>
      <td>1.3</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4.6</td>
      <td>3.1</td>
      <td>1.5</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5.0</td>
      <td>3.6</td>
      <td>1.4</td>
      <td>0.2</td>
    </tr>
  </tbody>
</table>
</div>

``` python
cluster_models = [
    cluster.KMeans,
    cluster.AffinityPropagation
]

model_kwargs_list = [
    {"n_clusters": [2, 3, 4], "init": ["k-means++", "random"]},
    {"damping": [0.6, 0.7, 0.8]}
]
```

``` python
grid_search(
    data_to_cluster=X,
    cluster_models=cluster_models,
    model_kwargs_list=model_kwargs_list,
    sort=True,
    highlight=True
)
```

    0it [00:00, ?it/s]
      0%|                                               | 0/6 [00:00<?, ?it/s]
    100%|███████████████████████████████████████| 6/6 [00:00<00:00, 57.06it/s]
    1it [00:00,  9.21it/s]
    100%|███████████████████████████████████████| 3/3 [00:00<00:00, 77.47it/s]
    2it [00:00, 13.37it/s]

<table id="T_1d0b1">
  <thead>
    <tr>
      <th class="blank level0" >&nbsp;</th>
      <th id="T_1d0b1_level0_col0" class="col_heading level0 col0" >cluster_model</th>
      <th id="T_1d0b1_level0_col1" class="col_heading level0 col1" >model_params</th>
      <th id="T_1d0b1_level0_col2" class="col_heading level0 col2" >avg_silhouette_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th id="T_1d0b1_level0_row0" class="row_heading level0 row0" >0</th>
      <td id="T_1d0b1_row0_col0" class="data row0 col0" >KMeans</td>
      <td id="T_1d0b1_row0_col1" class="data row0 col1" >{'init': 'k-means++', 'n_clusters': 2}</td>
      <td id="T_1d0b1_row0_col2" class="data row0 col2" >0.681046</td>
    </tr>
    <tr>
      <th id="T_1d0b1_level0_row1" class="row_heading level0 row1" >3</th>
      <td id="T_1d0b1_row1_col0" class="data row1 col0" >KMeans</td>
      <td id="T_1d0b1_row1_col1" class="data row1 col1" >{'init': 'random', 'n_clusters': 2}</td>
      <td id="T_1d0b1_row1_col2" class="data row1 col2" >0.681046</td>
    </tr>
    <tr>
      <th id="T_1d0b1_level0_row2" class="row_heading level0 row2" >1</th>
      <td id="T_1d0b1_row2_col0" class="data row2 col0" >KMeans</td>
      <td id="T_1d0b1_row2_col1" class="data row2 col1" >{'init': 'k-means++', 'n_clusters': 3}</td>
      <td id="T_1d0b1_row2_col2" class="data row2 col2" >0.552819</td>
    </tr>
    <tr>
      <th id="T_1d0b1_level0_row3" class="row_heading level0 row3" >4</th>
      <td id="T_1d0b1_row3_col0" class="data row3 col0" >KMeans</td>
      <td id="T_1d0b1_row3_col1" class="data row3 col1" >{'init': 'random', 'n_clusters': 3}</td>
      <td id="T_1d0b1_row3_col2" class="data row3 col2" >0.552819</td>
    </tr>
    <tr>
      <th id="T_1d0b1_level0_row4" class="row_heading level0 row4" >5</th>
      <td id="T_1d0b1_row4_col0" class="data row4 col0" >KMeans</td>
      <td id="T_1d0b1_row4_col1" class="data row4 col1" >{'init': 'random', 'n_clusters': 4}</td>
      <td id="T_1d0b1_row4_col2" class="data row4 col2" >0.498051</td>
    </tr>
    <tr>
      <th id="T_1d0b1_level0_row5" class="row_heading level0 row5" >2</th>
      <td id="T_1d0b1_row5_col0" class="data row5 col0" >KMeans</td>
      <td id="T_1d0b1_row5_col1" class="data row5 col1" >{'init': 'k-means++', 'n_clusters': 4}</td>
      <td id="T_1d0b1_row5_col2" class="data row5 col2" >0.497455</td>
    </tr>
    <tr>
      <th id="T_1d0b1_level0_row6" class="row_heading level0 row6" >7</th>
      <td id="T_1d0b1_row6_col0" class="data row6 col0" >AffinityPropagation</td>
      <td id="T_1d0b1_row6_col1" class="data row6 col1" >{'damping': 0.7}</td>
      <td id="T_1d0b1_row6_col2" class="data row6 col2" >0.474338</td>
    </tr>
    <tr>
      <th id="T_1d0b1_level0_row7" class="row_heading level0 row7" >8</th>
      <td id="T_1d0b1_row7_col0" class="data row7 col0" >AffinityPropagation</td>
      <td id="T_1d0b1_row7_col1" class="data row7 col1" >{'damping': 0.8}</td>
      <td id="T_1d0b1_row7_col2" class="data row7 col2" >0.468801</td>
    </tr>
    <tr>
      <th id="T_1d0b1_level0_row8" class="row_heading level0 row8" >6</th>
      <td id="T_1d0b1_row8_col0" class="data row8 col0" >AffinityPropagation</td>
      <td id="T_1d0b1_row8_col1" class="data row8 col1" >{'damping': 0.6}</td>
      <td id="T_1d0b1_row8_col2" class="data row8 col2" >0.345462</td>
    </tr>
  </tbody>
</table>
