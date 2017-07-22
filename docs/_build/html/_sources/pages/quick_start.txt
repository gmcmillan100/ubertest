# Doc[in] Quick Start Guide

![Workflow](file:///Users/emulhern/emulhern_trunk/docs/images/Sphinx_Workflow_white-01.png)

A Sphinx document resides in a `docs` folder and is managed inside the existing Engineering workflow. This Quick Start Guide explains how to set up and use Sphinx and the Markdown plugin for creating documentation.


## Set Up Sphinx and Markdown

### 1. Set Up Sphinx

Make a `docs` directory inside your MP and run the `sphinx-quickstart` ECL script. Accept all the default settings during the setup:

```    
cd mp_trunk
mkdir docs && cd docs
sphinx-quickstart
```

When done correctly, your `docs` directory should look like this:

```
[~/mp_trunk/docs]$ ls
Makefile	_static		conf.py		index.rst    _build		_templates
```	


### 2. Add the Markdown Plugin

To enable markdown support in Sphinx, open `conf.py` and add the following lines of code:

```
# Markdown support
from recommonmark.parser import CommonMarkParser

source_parsers = {
    '.md': CommonMarkParser,
}

# The suffix of source filenames.
source_suffix = ['.rst', '.md']
```
You can now create pages in your docs directory using the .md extension.


### 3. Set the Theme

In `conf.py`, set the [Read the Docs theme](https://github.com/rtfd/sphinx_rtd_theme). Find the line with `html_theme =` and replace it so that it reads:

```
html_theme = 'sphinx_rtd_theme'
```


### 4. Exclude Build Directory from Git

Open `.gitignore` in the trunk directory and add this line:

```
docs/_build
```


### 5. Configure Gradle to Find Docs

Open `settings.gradle` in the trunk directory. Delete the existing code and replace it with:

```
include 'docs'
```


### 6. Exclude the Docs Directory from Review Board

(Optional) Do this to exclude the `docs` directory from RB:

```
cd acl
touch exclude.acl
```

Open `exclude.acl` and add the directory path to exclude:

```
owners: [ 'exclude', 'gmcmilla', 'emulhern' ]
paths: [ 'docs/*' ]
```

In the owners section, you must list at least two people (it does not matter who) and the word `exclude`.


## Write Your Doc

### 1. Add Pages

Create a folder within `<mp>_trunk/docs` and name it *pages*. If you plan on using images in your doc, create a second folder within `<mp>_trunk/docs` and name it *images*.

```
cd mp_trunk/docs
mkdir pages
mkdir images
```

Inside the newly-created pages directory, you can create files for your documentation:

```
cd mp_trunk/docs/pages
touch new_file.md
touch new_file2.md
```


### 2. Markdown Basics

For a good overview of Markdown basics, take a look at [CommonMark's cheat sheet and interactive tutorial](http://commonmark.org/help/).

.. Note:: We're using the `Recommonmark Plugin <https://recommonmark.readthedocs.io/en/latest/>`_ to enable Markdown in Sphinx.

### 3. Set Up a Table of Contents in `index.rst`

If you want to include an auto-generated contents list, it’s important to keep the index file using the .rst extension instead of Markdown (.md). Note that a new line between :glob: and pages/* is required:

```
Contents:

.. toctree::
   :maxdepth: 1
   :glob:

   pages/*
```

If you do not want the table of contents to repeat at the top of your doc page, add `:hidden:` to your code:

```
.. toctree::
   :maxdepth: 1
   :hidden:
   :glob:

   pages/*
```


### 4. Workaround for Broken Tables in Current Plugin

Tables are broken in CommonMark's current version of the plugin. To include tables in your documentation, use raw HTML until a more permanent fix is implemented. For example:

```
<table style="width:100%">
  <tr>
    <th>Column 1</th>
    <th>Column 2</th>
    <th>Column 3</th>
  </tr>
  <tr>
    <td>cell 1</td>
    <td>cell 1</td>
    <td>cell 1</td>
  </tr>
  <tr>
    <td>cell 2</td>
    <td>cell 2</td>
    <td>cell 2</td>
  </tr>
</table>
```


### 5. Cross Referencing 

Cross referencing allows you to link to arbitrary locations in any document and can be a useful tool to avoid broken links. A more in-depth discussion of Cross Referencing is located here: :ref:`Cross Referencing`.


## Build and Preview the HTML

You can preview the HTML for your .md files. The `sphinx-build` script builds a Sphinx documentation set on your computer and allows you to preview the HTML before you publish it to the [Product Dashboard](https://tools.corp.linkedin.com/apps/tools/product-dashboard/admin/).


### 1. Build the HTML

In order to build your HTML, change to your docs directory and then run the `sphinx-build` command.

```
$ cd docs
$ sphinx-build -b html . _build/html
Running Sphinx v1.4.1
loading pickled environment... done
building [mo]: targets for 0 po files that are out of date
building [html]: targets for 1 source files that are out of date
updating environment: [config changed] 1 added, 0 changed, 0 removed
reading sources... [100%] index                                                                            
looking for now-outdated files... none found
pickling environment... done
checking consistency... done
preparing documents... done
writing output... [100%] index                                                                             
generating indices... genindex
writing additional pages... search
copying static files... done
copying extra files... done
dumping search index in English (code: en) ... done
dumping object inventory... done
build succeeded.
```


### 2. Previewing the HTML

Start your web browser. Go to **File > Open File** and then choose the file you want to preview. For example, **mp_trunk > docs >** _**build > html > pages > index.html**.

Once you have found the file you want to open, click **Open**.


## Publish the Doc

### 1. Configure `product-spec.json`

Make sure your `product-spec.json` file contains the following code:

```
"build": {
  "commands": {
    "test": "echo 'testing done by build command'",
    "snapshot": "ligradle -Psnapshot=true build",
    "build": "ligradle -Prelease=true -PallArtifacts build",
    "apidoc": "cd docs && make html && mkdir -p ../build/reports/apidoc/html && cp -r _build/html/* ../build/reports/apidoc/html"
  },
```


### 2. Add your docs to Git and publish to Review Board

Add your docs to Git and publish to RB, for example:

```
git add docs
git commit -m "Initial commit"
git-review create
git-review dcommit -r <rb-number>
git pull --rebase
git push
```


## Reference Links

For more advanced topics, see :ref:`autodoc`.

...see [Autodoc for APIs](https://tools.corp.linkedin.com/apps/tools/pd-data-service/api/report_data/docin/apidoc/report_file/html/docin-buildDocsHtml/pages/autodoc.html)

