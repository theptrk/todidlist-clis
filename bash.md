# todidlist with bash

## Getting dids
### Step 1: Create the bash script for "get"

First lets create a single directory where we will store our scripts `~/s`

```bash
$ mkdir ~/s
```

Next create a bash script in "~/s" (without an extension)
`$ touch ~/s/did`

Get your access token from `todidlsit.com/profile` and add this to your new file
```bash
#!/bin/bash

curl -L http://todidlist.com/api/dids/getrecent -X POST --post302 \
-d api_access_token=<your_access_token>
```

`-L` tells curl to follow redirects

`--post302` tells curl to follow redirects with a post request instead of a get

### Step 2: Add executable permissions to it

```bash
$ chmod u+x did
```

### Step 3: Add this directory to your $PATH
First, what is your current path? Run `echo $PATH` to find all the directories in your current `$PATH`

It will likely look something like this... (notice it doesn't include your new `~/s` directory)

`/usr/bin:/bin:/usr/sbin:/sbin:/usr/local/bin...`

Now lets append our new directory to $PATH in `bash_profile` or your favorite startup script

```bash
# in bash_profile

export PATH=$PATH:~/s
```

### Step 4: Try `did` in your command line
Now that scripts in your `~/s` directory will be executable, source your `bash_profile` if needed and run your new command

```bash
$ source ~/.bash_profile
$ did

# ====== DIDS DONE ======
# 🚀 made my bed - 17 hours ago
# 🚀 this works! - 17 hours ago
```

## Creating dids

Lets use the same executable and check if arguments have been passed in. 

This way `$ did` will still retrieve the Dids but `$ did made my bed` will create the Did "made my bed"

### Step 1: Add an if else block based on argument length 

```
#!/bin/bash

if [ $# -eq 0 ] ; then

echo "Getting Recent Dids..."
curl -L http://todidlist.com/api/dids/getrecent -X POST --post302 \
-d api_access_token=<your_access_token>

else

# TODO in Step 2

fi
```

### Step 2: Add logic that sends your command line arguments

Here is the the else block that will send your "Create Did" request.

```
# ...
else

echo "Sending Dids..."
curl -L http://todidlist.com/api/dids/create -X POST --post302 \
-d api_access_token=<your_access_token> \
-d did="$*"

fi
```

`$*` refers to the arguments you pass into this script

### Step 3: Try `did` in your command line

```bash
$ did I created my first bash script
```

## TLDR

This is your final `did` file

```
#!/bin/bash

if [ $# -eq 0 ] ; then

echo "Getting Recent Dids..."
curl -L http://todidlist.com/api/dids/getrecent -X POST --post302 \
-d api_access_token=2b33a414_4c71_44a1_95bc_8fc8d09c8d8a

else

echo "Sending Dids..."
curl -L http://todidlist.com/api/dids/create -X POST --post302 \
-d api_access_token=2b33a414_4c71_44a1_95bc_8fc8d09c8d8a \
-d did="$*"

fi
```
