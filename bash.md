# todidlist with bash

## Getting dids
### Step 1: create the bash script for "get"

First lets create a single directory where we will store our scripts `~/s`

```bash
$ mkdir ~/s
```

Next create a bash script in "~/s" (without an extension)
`$ touch ~/s/didget`

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
$ chmod u+x didget
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

### Step 4: try `didget` in your command line
Now that scripts in your `~/s` directory will be executable, source your `bash_profile` if needed and run your new command

```bash
$ source ~/.bash_profile
$ didget

# ====== DIDS DONE ======
# 🚀 made my bed - 17 hours ago
# 🚀 this works! - 17 hours ago
```

## Creating dids

This will be easier now that we have set up our path

### Step 1: Create the bash script for "get"

`$0` refers to the arguments you pass into this script

```bash
#!/bin/bash

curl -L http://todidlist.com/api/dids/create -X POST --post302 \
-d api_access_token=<your_access_token> \
-d $0
```
### Step 2: Add executable permissions to it

`chmod u+x did`

### Step 3: Try `did` in your command line

```bash
$ source ~/.bash_profile
$ did I created my first bash script
```


* potential future improvements
- create one single command that checks if arguments have been passed
