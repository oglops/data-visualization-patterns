# PYTHON IMPLEMENTATION 


## Data Set

For this example it was used Data Set called mtcars (Motor Trend Car Road Tests), which comes by default in R. This data was extracted from the 1974 Motor Trend US magazine, and comprises fuel consumption and 10 aspects of automobile design and performance for 32 automobiles (1973–74 models). 

To use this data set in Python, was used a Python module called rpy2. First create a file named as datos.py and write the next code.


~~~~{.python}
from rpy2.robjects import r
from rpy2.robjects import pandas2ri

def data(name):
        return pandas2ri.ri2py(r[name])
~~~~~~~~~~~~~



Then it is necessary import the datos.py file into the proyect, which you are working.


~~~~{.python}
from datos import data
d=data('mtcars')
~~~~~~~~~~~~~



## Dependences

* **rpy2** Python interface to the R language (Gautier, 2016)[^1]. The rpy2 package is used to access all R datasets from Python.
* **Matplotlib** is a python 2D plotting library which produces publication quality figures in a variety of hardcopy formats and interactive environments across platforms. matplotlib can be used in python scripts, the python and ipython shell, web application servers, and six graphical user interface toolkits (Hunter, 2016)[^2].
* **Seaborn** is a Python visualization library based on matplotlib. It provides a high-level interface for drawing attractive statistical graphics (Waskom,2013)[^3].
* **Pyqtgraph**  is a pure-python graphics and GUI library built on PyQt4 / PySide and numpy. It is intended for use in mathematics / scientific / engineering applications (Campagnola, 2014)[^4].


## Code Example


### Matplotlib


~~~~{.python}
import matplotlib.patches as p
import matplotlib.pyplot as plt
import pandas
import math
from datos import data

fig=plt.figure(1, figsize=(4,4))
ax = plt.subplot(111, aspect='equal')
colors=['#FF9999', 'lightskyblue','#66FF66' ]
d=data('mtcars')
ps = pandas.Series([i for i in d.gear])
counts = ps.value_counts()

x=0.05
y=0.9
m=0
cols=1
for i in counts:
        for j in range(i):
                p1 = p.Circle((x, y), 0.05, fc=colors[m],
edgecolor='white')
                x=x+0.1
                ax.add_patch(p1)
                cols=cols+1
                if (cols>10):
                        cols=1
                        x=0.05
                        y=y-0.1
        m=m+1
x=0.05
y=0.3
m=0
for i in counts.index:
        p2 = p.Circle((x, y), 0.05, fc=colors[m], edgecolor='white')
        ax.add_patch(p2)
        plt.text(x+0.17, y-0.03, str(int(i))+" gear", ha="center",
family='sans-serif', size=11, color='b' )
        #y=y-0.13
        x=x+0.35
        m=m+1

ax.axis('off')
plt.title("Dot Matrix by Number of Gears", color='b', family='sans-
serif', size=14)
plt.show()
~~~~~~~~~~~~~

![](figures/A33Dot_MatrixPy_figure3_1.png)


The complete online documentation is also available at [matplotlib](http://matplotlib.org/contents.html).


### Seaborn


~~~~{.python}
import matplotlib.patches as p
import matplotlib.pyplot as plt
import pandas
import seaborn as sns
from datos import data

sns.set(style="white")
colors = sns.husl_palette(10)

fig=plt.figure(1, figsize=(4,4))
ax = plt.subplot(111, aspect='equal')
d=data('mtcars')
ps = pandas.Series([i for i in d.gear])
counts = ps.value_counts()

x=0.05
y=0.9
m=0
cols=1
for i in counts:
        for j in range(i):
                p1 = p.Circle((x, y), 0.05, fc=colors[m],
edgecolor='white')
                x=x+0.1
                ax.add_patch(p1)
                cols=cols+1
                if (cols>10):
                        cols=1
                        x=0.05
                        y=y-0.1
        m=m+4
x=0.05
y=0.3
m=0
for i in counts.index:
        p2 = p.Circle((x, y), 0.05, fc=colors[m], edgecolor='white')
        ax.add_patch(p2)
        plt.text(x+0.17, y-0.03, str(int(i))+" gear", ha="center",
family='sans-serif', size=11, color='b' )
        x=x+0.35
        m=m+4

ax.axis('off')
plt.title("Dot Matrix by Number of Gears", color='b', family='sans-
serif', size=14)
plt.show()
~~~~~~~~~~~~~

![](figures/A33Dot_MatrixPy_figure4_1.png)


The online documentation is available in [Seaborn](https://stanford.edu/~mwaskom/software/seaborn/api.html).


### Pyqtgraph


~~~~{.python}
import pyqtgraph as pg
from  PyQt4  import  QtGui
import pandas
from datos import data

win = pg.GraphicsWindow("Dot Matrix ")
win.resize(300,300)
v = win.addViewBox()
v.setAspectLocked()
text = pg.TextItem("Dot Matrix by Number of Gears ",
anchor=(-0.1,22.5), color='w')
v.addItem(text)
d=data('mtcars')
ps = pandas.Series([i for i in d.gear])
counts = ps.value_counts()
position=[ (-0.5,15), (-2,15), (-3.5,15)]
colours = [QtGui.QColor('springgreen'), QtGui.QColor('lightskyblue'),
QtGui.QColor('lightcoral')]

x=0.0
y=1.0
m=0
cols=1

for i in counts:
        for j in range(i):
                ellipse = QtGui.QGraphicsEllipseItem(x,y,0.05,0.05)
                ellipse.setBrush(colours[m])
                v.addItem(ellipse)
                x=x+0.05
                cols=cols+1
                if (cols>10):
                        cols=1
                        x=0.0
                        y=y-0.05
        m=m+1

x=0
y=0.7
m=0
for i in counts.index:
        ellipse = QtGui.QGraphicsEllipseItem(x,y,0.05,0.05)
        ellipse.setBrush(colours[m])
        v.addItem(ellipse)
        x=x+0.15
        m=m+1
j=0
for x in counts.index:
    text = pg.TextItem(str(int(x))+" gear", anchor=(position[j]),
color='w')
    v.addItem(text)
    j+=1

if __name__ == '__main__':
    import sys
    if (sys.flags.interactive != 1) or not hasattr(QtCore,
'PYQT_VERSION'):
        QtGui.QApplication.instance().exec_()
~~~~~~~~~~~~~

![](figures/A33Dot_MatrixPy_figure5_1.png)


The complete online documentation is also available at [Pyqtrgaph](http://www.pyqtgraph.org/documentation/).


### References

[^1]: Gautier, Laurent (2016). rpy2. Consultado el 01 de Febrero, 2016 en http://rpy2.bitbucket.org/
[^2]: Hunter, John (2016). matplotlib. Consultado el 03 de Febrero, 2016 en http://matplotlib.org/
[^3]: Waskom, Michael (2016). Seaborn. Consultado el 08 de Febrero, 2016 en https://stanford.edu/~mwaskom/software/seaborn/index.htmltest/
[^4]: Campagnola, Luke (2014). Pyqtgraph. Consultado el 10 de Febrero, 2016 http://www.pyqtgraph.org/
