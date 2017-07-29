### How to create a ilastik environment with conda

* Download or checkout the file 'ilastik_env_package_list_export.txt' from the 'python3-win' branch of https://github.com/ilastik/ilastik-build-conda
* Use the following command (you can change the name of the environment if you want):
    conda create --name ilastik_env --file ilastik_env_package_list_export.txt --override-channels -c defaults -c conda-forge -c DavidStronczek
* Confirm the installation. This make take a while.
* Download or checkout the branch qt5py3 of the ilastik-meta repo into the conda environment:
    cd path\to\conda\envs\ilastik_env\
    git clone https://github.com/ilastik/ilastik-meta
	cd ilastik-meta
	git checkout qt5py3
	git submodule update --init --recursive
* TEMPORARY FIX: Fix a bug in the file ilastik-meta/ilastik/ilastik/workflows/__init__.py. Change line 67
    > from .tracking.structured.structuredTrackingWorkflow import StructuredTrackingWorkflowFromBinary
  to include the second import
    > from .tracking.structured.structuredTrackingWorkflow import StructuredTrackingWorkflowFromBinary, StructuredTrackingWorkflowFromPrediction
  This should be fixed in future ilastik versions.
* Compile the python code with the python in your ilastik environment. In ilastik-meta execute the following command:
	activate ilastik_env
	python -m compileall lazyflow volumina ilastik
* Download or checkout the file 'ilastik-meta.pth' from the 'python3-win' branch of https://github.com/ilastik/ilastik-build-conda and copy it into your conda environment into the folder '\Lib\site-packages\'
* Download or checkout the file 'default_ilastikrc' from the 'python3-win' branch of https://github.com/ilastik/ilastik-build-conda and copy it into your home folder (c:\users\YourName\) as '.ilasticrc'
* In the folder path\to\conda\envs\ilastik_env\ilastik-meta\ilastik execute the following to start ilastik
	python ilastik.py
