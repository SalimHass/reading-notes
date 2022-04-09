# Data Analysis
## Jupyter Lab
JupyterLab is a next-generation web-based user interface for Project Jupyter.

JupyterLab enables you to work with documents and activities such as Jupyter notebooks, text editors, terminals, and custom components in a flexible, integrated, and extensible manner.

You can arrange multiple documents and activities side by side in the work area using tabs and splitters. Documents and activities integrate with each other, enabling new workflows for interactive computing, for example:

- Code Consoles provide transient scratchpads for running code interactively, with full support for rich output. A code console can be linked to a notebook kernel as a computation log from the notebook, for example.

- Kernel-backed documents enable code in any text file (Markdown, Python, R, LaTeX, etc.) to be run interactively in any Jupyter kernel.

- Notebook cell outputs can be mirrored into their own tab, side by side with the notebook, enabling simple dashboards with interactive controls backed by a kernel.

- Multiple views of documents with different editors or viewers enable live editing of documents reflected in other viewers. For example, it is easy to have live preview of Markdown, Delimiter-separated Values, or Vega/Vega-Lite documents.

JupyterLab also offers a unified model for viewing and handling data formats. JupyterLab understands many file formats (images, CSV, JSON, Markdown, PDF, Vega, Vega-Lite, etc.) and can also display rich kernel output in these formats. See File and Output Formats for more information.

To navigate the user interface, JupyterLab offers customizable keyboard shortcuts and the ability to use key maps from vim, emacs, and Sublime Text in the text editor.

JupyterLab extensions can customize or enhance any part of JupyterLab, including new themes, file editors, and custom components.

JupyterLab is served from the same server and uses the same notebook document format as the classic Jupyter Notebook.

## NumPy
numpy is a python data analysis package , with it you can speed up the workflow , and interface with other pachages in the python ecosystem.

to start ,you need to read the csv file containing the data, we use the syntax `with open ("filename.csv , "r") as name)`
`data = list(csv.reader(name,delimiter=';'))` 

now you have the data as list of lists that represents a table. 

### Numpy 2-dimensional array
with numpy you work with multidimensional arrays. A 2-dimensional array is also known as a matrix. in numpy the number of dimensions is called the rank, each dimension is called axis . 
### creating a NumPy array
we can create numpy array using numpy.array function.  If we pass in a list of lists, it will automatically create a NumPy array with the same number of rows and columns.One of the limitations of NumPy is that all the elements in an array have to be of the same type, so if we include the header row, all the elements in the array will be read in as strings.

to import numpy we use `import numpy as np` and to set the data as a list ` data= np.array(data[1:], dtype=np.float)`
this code will exclude the first row "the header" beacuse it containes strings, and will change the number to float to make calculations easier.

use `data.shape` to check the number of (rows, coulmns),

#### creating array methods
you can use this code `array=np.zeros((3,4))` will creat an an array with row and four columns , every element in this array will contain 0

you can use `np.random.rand((3,4))` to fill a 3 rows and 4 coulmns array with random numbers.

### using numpy to read in files
numpy can read csv files directly ot other files into array, we can do this by using  numpy.genfromtxt function. 
we use `data = np.genfromtxt("filename.csv", delimiter=";", skip_header=1)` to read a filename , the delimiter for the data to be parsed proparly , and skip_header=1 to specify wich row is the header to be skipped.

we can slice the array just like normal lists `data[0:3,3]`

### NumPy Array Methods

In addition to the common mathematical operations, NumPy also has several methods that you can use for more complex calculations on arrays. An example of this is the numpy.ndarray.sum method. This finds the sum of all the elements in an array by default

- numpy.ndarray.mean — finds the mean of an array.
- numpy.ndarray.std — finds the standard deviation of an array.
- numpy.ndarray.min — finds the minimum value in an array.
- numpy.ndarray.max — finds the maximum value in an array.

### NumPy Array Comparisons

NumPy makes it possible to test to see if rows match certain values using mathematical comparison operations like <, >, >=, <=, and ==

