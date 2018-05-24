# Fundamentals

## Applying Deep Learning

- Examples
  - [Fast Style Transfer](https://github.com/lengstrom/fast-style-transfer)
  - [MIT Deep Traffic](https://selfdrivingcars.mit.edu/deeptrafficjs/)
  - [Deep Learning Flappy Bird](https://github.com/yenchenlin/DeepLearningFlappyBird)

## Anaconda

### Packages

- `conda install numpy scipy pandas`
- `conda remove package_name`
- `conda update package_name`
- `conda update --all`
- `conda list`

### Environments

- `conda create -n env_name list of packages`
  - `conda create -n my_env numpy`
- `source activate my_env`
- `(my_env) ~ $` in terminal prompt
- `conda list show installed packages in environment`
- `conda install package_name`
  - Will only be available in environment
- `source deactivate to leave environment`
- `conda env export`
  - Writes out packages in environment
- `conda env export > environment.yaml`
  - Export environment as YAML file
- `conda env create -f environment.yaml`
  - Creates environment from file with same name
- `conda env list`
  - Shows all environments created, root is default environment
- `conda env remove -n env_name`
  - Removes specific environment
- `conda install nb_conda`
  - Manage environments from within Jupyter from Conda tab
- `pip freeze > requirements.txt`
  - Exports list of packages in environment to file

## Jupyter Notebook

- Type `jupyter notebook` in terminal to launch notebook

### Shortcuts

- <kbd>H</kbd> - show all shortcuts
- <kbd>A</kbd> - new cell above current
- <kbd>B</kbd> - new cell below current
- <kbd>Y</kbd> - change from Markdown to code cell
- <kbd>M</kbd> - switch from code to Markdown cell
- <kbd>L</kbd> - turn on line numbers
- <kbd>D</kbd> + <kbd>D</kbd> - delete cell
- <kbd>S</kbd> - save notebook
- <kbd>Shift</kbd> + <kbd>CMD</kbd> + <kbd>P</kbd> - open command palette

### Magic Keywords

- Preceded with % or %%
- `%timeit some_function(20)`
  - Shows time some_function took to run
- `%%timeit at beginning of cell`
  - Shows how long cell took to run
- `%matplotlib inline` to render image in notebook
  - `%config InlineBackend.figure_format = 'retina'` in addition renders in higher resolution e.g. for retina displays
- `%pdb` turns on interacitve debugger
  - Inspects variables in current namespace
  - Enter `q` in prompt to quit debugger

### Use LaTeX

- [Udacity Primer](http://data-blog.udacity.com/posts/2016/10/latex-primer/) on using LaTeX in Jupyter Notebook

## Ressources

- [Grokking Deep Learning](https://www.manning.com/books/grokking-deep-learning) by Andrew Trask
- [Neural Networks and Deep Learning](http://neuralnetworksanddeeplearning.com)
- [Deep Learning Book](http://www.deeplearningbook.org)
- [Decentralized Applications](http://moscowglobalforum.ru/upload/iblock/88a/88a484da83063f94ca67bdf9ab077d5d.pdf) by Siraj Raval
- [Andreessen Horowitz Primer](https://vimeo.com/170189199)
- [TensorFlow Playground](http://playground.tensorflow.org/)
- Jupyter built–in [magic commands](http://ipython.readthedocs.io/en/stable/interactive/magics.html)

# Recurrent Neural Networks (RNNs)

- Used and speech recognition and translation
- Previous feedforward neural networks were trained using only current inputs, not considering previous inputs, no memory elements
- RNN use memory, meaning past inputs when producing current output
- Can capture temporal dependencies 

### Vanishing Gradient Problem

- Capturing relationships that span more then 10 steps back is impossible due to decrease of contibution of information over time
- Due to backpropagation, which adjustes weights using gradients; gradients calculated by continuous multiplication of derivates; derivates might be so small that multiplication may cause gradient to vanish
- Solution: Use Long Short-Term Memory Networks (LSTMs) or Gated Recurrent Units (GRU)

## Long Short-Term Memory Networks

- Option to overcome vanishing gradient problem in RNNs
- Examples: voice assistants (Alexa), traffic predictions (Waze), movie recommendations (Netflix), stock price predictions (hedge funds), natural language processing (Google Translate)

## Ressources 

- [Elman Network Publication](https://onlinelibrary.wiley.com/doi/abs/10.1207/s15516709cog1402_1)

# General Adversarial Networks (GANs)

- Used to create completely new, realistic images after learning from set of images
- Stackgan model: takes textual description of bird and generates photo of bird matching description
- Pix2Pix: Takes sketch as input and generates realistic image from drawing
- Not limited to visuals

*To be continued*
