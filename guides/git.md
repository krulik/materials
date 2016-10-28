# Git & Github Guide

## Intro

Git is a version control system (VCS), with a few differentiating points:

1. It's fast
1. It's distributed (there's no need for a central server as every client posses the whole history for a repository)
1. Its rooted in the open source community and therefore integrates very well with other tools in our workflow

## Tutorial

There's a short and sweet tutorial by Codeacademy and Github called "Try Git".
It's assumed you'll complete it before proceeding any further.

https://try.github.io/

## Push your first repo to Github

### Initialize a local repository

Assuming you're inside a folder called `/my-repo` with the files you'd like to push.

```
# initialize a new git repository in /my-repo, so git will start tracking your files

$ git init

Initialized empty Git repository in /my-repo
```

### Initialize a repository on Github

Now you should do the equivalent step on Github servers.

Go to your profile on Github and create a new repository.
You'll need to provide a name. It's advised you'll use the same name as your folder name (`my-repo`).

**IMPORTANT**

Don't check any checkboxes that add a `README.md`, `.gitignore` or `LICENSE` files to the repo. It needs to be empty.

### Add the Github repository as a `remote` in your local repository

Replace `yourusername` and `my-repo` in the following URL with the corresponding values.

```
$ git remote add origin https://github.com/yourusername/my-repo.git
```

You can test that the remote was added correctly by typing `git remote -v` and seeing `origin` there with the above URL.

`-v` stands for verbose, otherwise it won't output the URL.

### Commit your local state

You should type `git status` and see that you have untracked files (Git will mark them as untracked and with a red color). These are files that Git had detected in your folder which he doesn't have any record about. You should first add them to Git:

```
# add all files in the folder

$ git add .
```

Now if you type `git status` you'll see the files marked as "new" and with a green color. If everything's ok you can commit the state:

```
$ git commit -m "initial commit"
```

`-m` stands for a commit message, you must provide one and make sure it's meaningful.

### Push your local branch to the remote branch

```
$ git push -u origin master
```

`-u` (upstream) connects your local branch with the remote branch for future push (and pull) so you can write only `git push`.

You can go to your Github repository, refresh the page and see the contents of your folder on Github servers.

:tada:

## Github pages

Github can automatically publish your site on the Web, with a CDN and even a custom domain name for free.

All you need to do is create and push into a special branch that's monitored by Github and when you push a deploy is triggered.

### Create a Github pages branch

Create a new branch with the name `gh-pages` (must be spelled exactly) and immediately switch to it:

```
$ git checkout -b gh-pages
```

The `checkout` command switches to a branch and the `-b` flag creates it.

**NOTICE**

Git branches are mere pointers to a state of your repository (a commit), and when you create a new branch it will point initially to the same state as the original branch (`master` in this case).

### Push the new branch to Github servers

You don't need to create the branch on Github servers first, it'll be created automatically when you push.

```
$ git push -u origin gh-pages
```

### Test the deployment

After you push to `gh-pages` Github publishes the site under this URL:

```
http://yourusername.github.io/my-repo
```

You should replace `yourusername` and `my-repo` with the corresponding values.

Open the browser and witness the magic :simple_smile: :sparkles:
