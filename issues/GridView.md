# GridView Issue

## Q1: GridView can't sync the backend users including adding and deleting

Step:

1. Check the UID of users, which must be smaller than 60000 and bigger than 1000, otherwise the GridView can't show the users normally. (in the /etc/passwd/)
2. If the ```clusconf``` can't be excuted, please re-install the clusconf
	+ ```scp``` the clusconf.tar.gz to the linux system
	+ unzip it
	+ ```cd``` into the unziped dir and run ```./install.sh```

