This tutorial is about how to run matlab engine in the python 3.6.

Requirement:
+ Matlab 2018a
+ Python 3.6

# Install Matlab Locally

Steps:
1. Download the iso file and crack file. 
2. Modify the installer_inputs.txt with your local path and destination path.
3. Install. ```./install -inputfile ./installer_input.txt -mode silent```
4. Activate with crack file.

# Use the Matlab Engine in Python3.6

Steps:
```bash
cd matlabpath/extern/python
python3 setup.py install
```

Check: 
https://www.mathworks.com/help/matlab/matlab_external/call-matlab-functions-from-python.html

Note: 
The ```import matlab.engine``` must locate at the head of python scripts.

