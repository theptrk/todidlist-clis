# todidlist with bash

## getting dids
### step 1: create the bash script for "get"

First we're going to create a directory called "s" (for scripts) in our root directory
`mkdir ~/s`

- New create a bash script in "~/s"
`touch ~/s/didget`

- Add this to your new file and input your access token from `todidlist.com/profile`
```bash
#!/bin/bash

curl -L http://todidlist.com/api/dids/getrecent -X POST --post302 \
-d api_access_token=<your_access_token>
```

`-L` tells curl to follow redirects

`--post302` tells curl to follow redirects with a post request instead of a get

### step 2: add executable permissions to it

`chmod u+x didget`

### step 3: add this directory to your $PATH
Run `echo $PATH` to find all the directories in your current `$PATH`

It will likely look something like this

`/usr/bin:/bin:/usr/sbin:/sbin:/usr/local/bin...`

Lets add a new path in `bash_profile` or your favorite startup script

```bash
# in bash_profile

export PATH=$PATH:~/s
```

Now every script in your `~/s` directory will be executable

### step 4: try `didget` in your command line
`$ didget`

## creating dids

This will be easier now that we have set up our path

### step 1: create the bash script for "get"

`$0` refers to the arguments you pass into this script

```bash
#!/bin/bash

curl -L http://todidlist.com/api/dids/create -X POST --post302 \
-d api_access_token=<your_access_token>
-d $0
```
### step 2: add executable permissions to it

`chmod u+x did`

### step 3: try `did` in your command line

`$ did I created my first bash script`


* potential future improvements
- create one single command that checks if arguments have been passed
