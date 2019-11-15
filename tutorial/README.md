# Basic Command for Linux

1. Log in the server
    + Use ```ssh``` in terminal of your computer
        * ```ssh -p 2222 username@IP```
        * Note: pls use the campus network or use VPN to access campus network
        * The password is invisible! Once you finish, just click ENTER of keyboard. 
    + Or use softwares, for example, putty, Xshell, etc.
2. Log out the server
    +  Exit the terminal or software of your computer
    +  Type ```exit``` in terminal
3. Make a new directory
    + ```mkdir dirname```
4. Make a new file
    + ```touch test.txt```
5. Edit a file
    + ```vim test.txt```
    + Insert mode ```i```
    + Save and quit vim ```:wq```
    + Quit vim and not save ```:q!```
6. Print a file
    + ```cat test.txt```

# Node and PBS Queue System of the Server

1. Nodes: in the server, there are multi-nodes, and each node can be regarded a computer. In our server, each node except gpu includes 20 cpu cores. And the gpu node has 28 cpu cores and 8 gpu cores.
    + Check status of each node ```pestat```
    + Check the status and basic information of gpu node (Make sure login gpu node previously ```ssh node100```)
        * Get cuda version ```nvcc -V```
        * Get status of each gpu core ```nvidia-smi```
2. PBS queue: there are two major methods for off-line running your script or command. First one is ```nohup``` + your command, such as installing a python package in the back-end with ```nohup pip3 install package```. The second is exactly the PBS queue system. Your script should be submitted into the queue system to obtain an advanced management of the computation sources, such as data and model parallelism, batch testing, etc. For example, we have a python script named as ```test.py```. (If your script is cpu version, you can submit it to any queue, but if gpu version, you have to submit it into the gpu queue). Then we want to use 4 cores to accomplish the parallelism. And the PBS is all you need to run your script. The template of the pbs submission script is in [template.pbs](./template.pbs). Once you get the pbs script and your main file prepared, you can use the following command to accomplish your mission:
    + Submit the pbs script ```qsub template.pbs```
    + Check the status ```qstat``` and ```pestat```
    + And the process will be printed into a file ```*.o```
    + Kill your pbs mission ```qdel```+ID (Each submitted task has a unique ID)
    + Note: if you want to submit batch tasks related to a same main script, which always occurs in the hyper-parameters tuning or different data & model test, you can use a good-formatted template of script with ```${param}``` in your script, and submit them one shot with python in following code:
    ```python
    import subprocess
    qsub_command = """qsub -v param={0} template.sh""".format(param) # strip the tail '.csv'
    exit_status = subprocess.call(qsub_command, shell=True)
    ```

# Python Related Command

1. You can install a local python. Detail methods pls google it.
    + Note: pls use Python 3.x version
2. Install packages of python
    + ```pip install --user packagename```
3. Source your own environment
    + ```source activate.sh``` (activate.sh is your own activation file)
4. If you want to install gpu version of package, pls ```ssh node100``` (login gpu node) and run step 2.
    
# Shutdown and Restart the Server

1. Use the script of shutdown
2. If the server is out of control, we should shutdown it by force
    + Shutdown (turn down) process:
        * Computation node
        * Controller node (253 node) and IO node
        * Storage node
    + Restart (turn on) process:
        * Storage node
        * Controller node (253 node) and IO node
        * Computation node

# Run Remote Jupyter Notebook

1. Run the remote jupyter without browser ```jupyter notebook --no-browser --port=X```
2. Connect the local jupyter port and remote one with ```ssh -p 2222 -N -f -L localhost:Y:localhost:X username@IP```
3. Open the local website ```http://localhost:Y```

+ Close the local port
1. Find the PID of certain port ```lsof -i :port```
2. Kill the process ```kill -9 <PID>```





