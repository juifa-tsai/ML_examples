# Chapter 2 : Basic models of machine learning
This chapter give the introduction about the basic machine learning (ML) and start from classification case: ***linear perceptron***, ***adoptive linear perceptron*** and ***gradient decent algorithm*** etc. Before going to next chapter to using online open-source ML package, **scikit-learn**, we build the own ML class by **pandas** and **numpy** package. We also perform and visisulize the results with **matplotlib** and **ipython** packges. This is not only focusing on implement part but demonstrate the detail caculation and theories behinde the models. Some exmaples also give the optimaztion test which extends from the book. The exercises are all using iris data.  

1. [**Example 1 - Perceptron Linear Algorith, PLA**](https://nbviewer.jupyter.org/github/juifa-tsai/workbook_MachineLearning/blob/master/Python_Machine_Learning_RS/Chapter_02/example_01_PLA.ipynb?flush_cache=true)
   - Apply `Perceptron` to data iris data, to demonstrate the learing process.
2. [**Example 2 - PLA with shuffled data**](https://nbviewer.jupyter.org/github/juifa-tsai/workbook_MachineLearning/blob/master/Python_Machine_Learning_RS/Chapter_02/example_02_PLA.ipynb?flush_cache=true)
3. [**Example 3 - Ensembling PLA hypotheses**](https://nbviewer.jupyter.org/github/juifa-tsai/workbook_MachineLearning/blob/master/Python_Machine_Learning_RS/Chapter_02/example_03_PLA.ipynb?flush_cache=true)
4. [**Example 4 - Adaptive Linear Neuron Gradian Decent**](https://nbviewer.jupyter.org/github/juifa-tsai/workbook_MachineLearning/blob/master/Python_Machine_Learning_RS/Chapter_02/example_04_AdalineGD.ipynb?flush_cache=true)
5. [**Example 5 - Stochastic Gradian Decent**](https://nbviewer.jupyter.org/github/juifa-tsai/workbook_MachineLearning/blob/master/Python_Machine_Learning_RS/Chapter_02/example_05_StochasticGD.ipynb?flush_cache=true)

---
###### Correspoding example codes
* Chapter 2 @ [Chapter_02](.)
* Example 1 @ [example_01_PLA.ipynb](example_01_PLA.ipynb)
* Example 2 @ [example_02_PLA.ipynb](example_02_PLA.ipynb)
* Example 3 @ [example_03_PLA.ipynb](example_03_PLA.ipynb)
* Example 4 @ [example_04_AdalineGD.ipynb](example_04_AdalineGD.ipynb)
* Example 5 @ [example_05_StochasticGD.ipynb](example_05_StochasticGD.ipynb)

:warning: **If the example code (`*.ipynb`) can't be loaded, please *"copy"* its Github URL and *"paste"* to [nbviewer](https://nbviewer.jupyter.org) :warning:**

###### Functions and classes  
* [Perceptron.py](Perceptron.py) : class `Perceptron` for perceptron algorithm. \
* [Perceptron_online.py](Perceptron_online.py) : class `Perceptron_online` \
* [AdalineGD.py](AdalineGD.py) : class `AdalineGD` \
* [AdalineGD_online.py](AdalineGD_online.py) : class `AdalineGD_online` \
* [plot_decision_regions.py](plot_decision_regions.py) : function `plot_decision_regions`

---

### Perceptron algorithm
* It is online method, i.e. update weighting in each data point.
  ```
  X : array of variables
  w : array of weighting
  y : binary results
  ```
  ```
  z = w.X
  y = sign(z), i.e. 1 or -1
  ```

* Update weighting in each data point when ``y != y_true``.<br />
  ```
  w' = w + dw
     = w + eta.dy.X
  dw = eta.dy.X
     = eta.( y_true - y ).X
  ```
  1. ``dy.X`` : Fixing the wrong angle (too big/small) by extending/subtracting the normal vector of hyperplane ``w``. When whole dataset having zero of this, the hyperplane can classify the data in correct side.<br />
  2. ``eta``  : The training rate.

* Stop iteration<br />
When statistics of dataset is big enough, the algorithm can stop when ``dw = 0``, while the small statistics is using whole dataset with many iterations.  
  1. When ``dw = 0``.
  2. Linear separable.

### Class ``Perceptron``
@ Perceptron.py
* Global values
   * Parameters<br />
  ``eta`` : (**float**) Learning rate.<br />
  ``n_iter`` : (**int**) Passes over the training datasets (iteration).
   * Attributes<br />
  ``w_`` : (**1d-array**) Weights after fitting.<br />
  ``errors_`` : (**list**) # of misclassifications in every epoch.
* Functions
  * ``fit (X, y)`` : The functions for doing perceptron learning iteratively. <br />
  * ``net_input (X)`` : Calculate ``z = w.X = w'.X' + w_0.X_0, (X_0 = 1)``<br />
  * ``predict (X)`` : Get predict sign of y as`` y = sign(w.X)`` <br />
