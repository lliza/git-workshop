What is Git ?
=============

Git is a *distributed* **version control** system [1]

[1] <a href="http://git-scm.com/about">http://git-scm.com/about</a>

Getting Git
-----------

Some house-cleaning here. We assume of course you have Git installed,
(hopefully \>= 1.7.0).

If you don't you can install it from downloads on the git homepage or you can
install [Github's git GUI](https://help.github.com/articles/set-up-git/).

Setup
-----

As we're going to use `Github` during this workshop. Create a Github account on `http://www.github.com/` if you don't have one yet.

If you've created an account, open your terminal and type:
`cd ~/.ssh && ssh-keygen`

Press ENTER twice if you don't want to set a password for now, but otherwise follow the instructions in your terminal, until you'll receive a key (you'll see something with [RSA 3072] ending with [SHA256] and then some characters below).
Now type:

On OS X run: `cat id_rsa.pub | pbcopy`

On Linux run: `cat id_rsa.pub | xclip`

On Windows (via Cygwin/Git Bash) run: `cat id_rsa.pub | clip`

Now go to your Github account, click on the user icon in the right top menu, and click on `settings`.
Here click on `SSH and GPG keys`.

Click on `New SSH Key`. By `Title` enter what computer you're using and to identify for what you're using it. Such as: Mac Sogeti Jeroen
In the Key, you paste what you just copied: CTRL + V (or mac: CMD + V).

First thing to do is to setup your identity. This identifies you to
other people who download the project.

    $ git config --global user.name "Your Name"
    $ git config --global user.email your.email@example.com

Use the email address you used to sign up for Github!

As a helpful step, you may want to set Git to use your favourite editor
But you can skip this for now.

    $ git config --global core.editor emacs

Starting your journey
---------------------

First, clone this repository:
Go to the `documents` folder in your computer, and create there a new folder: "`Workspaces`". Open that folder.

Open your `terminal` and go to this folder, or simply (on Windows) typ into the folder address: "`cmd`" to open it in that location.

Now clone the project into this folder by entering the following command:

    $ git clone git@github.com:JeroenEgelmeers/git-workshop.git

Once you have cloned your repository, you should now see a directory
called `git-workshop`. This is your `working directory`

    $ cd git-workshop
    $ ls

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)
Stuck? Ask for help from the workshop staff

For the curious, you should also see the `.git` subdirectory. This is
where all your repository’s data and history is kept.

    $ ls -a .git

You will see :

    branches  config  description  HEAD  hooks  info  objects  refs

The staging area
----------------

Now, let’s try adding some files into the project. Create a couple of
files.

Let’s create two files named `bob.txt` and `alice.txt`. You can do this by using the command below, or simple just create them in the folder by adding the files manually.

    $ touch alice.txt bob.txt

Let’s use a mail analogy.

In Git, you first add content to the `staging area` by using `git add`.
This is like putting the stuff you want to send into a cardboard box.
You finalize the process and record it into the git index by using
`git commit`. This is like sealing the box - it’s now ready to send.

Let’s add the files to the staging area

    $ git add alice.txt bob.txt

Committing
----------

You are now ready to commit. The `-m` flag allows you to enter a message
to go with the commit at the same time.

    $ git commit -m "Added alice.txt and bob.txt for later use"

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)
Stuck? Ask for help from the workshop staff

Let’s see what just happened
----------------------------

We should now have a new commit. To see all the commits so far, use
`git log`

    $ git log

The log should show all commits listed from most recent first to least
recent. You would see various information like the name of the author,
the date it was committed, a commit SHA number, and the message for the
commit.

You should also see your most recent commit, where you added the two new
files in the previous section. However, git log does not show the files
involved in each commit. To view more information about a commit, use
`git show`.

    $ git show

You should see something similar to:

    commit 5a1fad96c8584b2c194c229de7e112e4c84e5089
    Author: Jeroen Egelmeers 
    Date:   Sun Aug 03 19:13:42 2022 +1200

        I am adding two new files

    diff --git a/alice.txt b/alice.txt
    new file mode 100644
    index 0000000..e69de29
    diff --git a/bob.txt b/bob.txt
    new file mode 100644
    index 0000000..e69de29

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)
Stuck? Ask for help from the workshop staff

A necessary digression
----------------------

In this section, we are going to add more changes, and try to recover
from mistakes.

Be forewarned, this next step is going to be hard. We will need to add
some content to alice.txt.

Open `alice.txt` and type in your favourite line from a song, or:

e.g. Lorem ipsum Sed ut perspiciatis, unde omnis iste natus error sit
voluptatem accusantium doloremque laudantium

Then **save** the file

What did we change? A very useful command is `git diff`. This is very
useful to see exactly what changes you have done.

    $ git diff

You should see something like the following:

    diff --git a/alice.txt b/alice.txt
    index e69de29..2aedcab 100644
    --- a/alice.txt
    +++ b/alice.txt
    @@ -0,0 +1 @@
    +Lorem ipsum Sed ut perspiciatis, unde omnis iste natus error sit voluptatem accusantium doloremque laudantium

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)
Stuck? Ask for help from the workshop staff

Staging area again
------------------

Now let’s add our modified file, `alice.txt` to the staging area. Do you
remember how? If not, please scroll back up to see how we did the staging part.

Next, check the `status` of `alice.txt`. Is it in the staging area now?

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)
Stuck? Ask for help from the workshop staff

Undoing
-------

Let’s say we did not like putting Lorem ipsum into `alice.txt`. One
advantage of a staging area is to enable us to back out before we
commit - which is a bit harder to back out of. Remembering the mail
analogy - it’s easier to take mail out of the cardboard box before you
seal it than after.

Here’s how to back out of the staging area :

    $ git reset HEAD alice.txt

    Unstaged changes after reset:
    M   alice.txt

Compare the `git status` now to the git status from the previous
section. How does it differ?

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)
Stuck? Ask for help from the workshop staff

Your staging area should now be empty. What’s happened to the Lorem
Ipsum changes? It’s still there. We are now back to the state just
before we added this file to staging area. Going back to the mail
analogy, we just took our letter out of the box.

Undoing II
----------

Sometimes we did not like what we have done, and we wish to go back to
the last *recorded* state. In this case, we wish to go back to the state
just before we added the Lorem ipsum text to `alice.txt`.

To accomplish this, we use `git checkout`, like so:

    $ git checkout alice.txt

You have now un-done your changes. Your file is now empty.

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)
Stuck? Ask for help from the workshop staff

Branching
---------

Most large code bases have at least two branches - a ‘master’ or 'main' branch and a
‘development’ branch. The main branch is code which is OK to be deployed
on to a website, or downloaded by customers. The development branch
allows developers to work on features which might not be bug free. Only
once everyone is happy with the development branch would it be merged
with the main branch.

Creating a branch in Git is easy. The `git branch` command, when used by
itself, will list the branches you currently have

    $ git branch

The `*` should indicate the current branch you are on, which is
`main`.

If you wish to start another branch, use
`git checkout -b (new-branch-name)` :
Let's create a branch on this repository, that contains your name so we can work on that branch.
So for example, my name is Jeroen Egelmeers, where `Jeroen` is my firstname, and `Egelmeers` is my lastname.
So I will do:

    $ git checkout -b jeroen-egelmeers

Try git branch again to check which branch you are currently on:

    $ git branch
      jeroen-egelmeers
    * main

The new branch is now created. Now let’s work in that branch. To switch
to the new branch:

    $ git checkout jeroen-egelmeers

`git checkout (branch-name)` is used to switch branches.

Let’s perform some commits now,

    $ echo 'some content' > test.txt
    $ git add test.txt
    $ git commit -m "Added experimental txt"

Now, let’s compare them to the develop branch. Use `git diff`

    $ git diff main

Basically what the above output says is that `test.txt` is present on
the `jeroen-egelmeers` branch, but is absent on the `develop` or `main` branch.

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)
Stuck? Ask for help from the workshop staff

Now you see me, now you don’t
-----------------------------

Git is good enough to handle your files when you switch between
branches. Switch back to the `main` branch

Try switching back to the main branch (Hint: It’s the same command we
used to switch to the branch with your name above)

Now, where’s our `test.txt` file ?

    $ ls
    README.textile  alice.txt   bob.txt     alpher.txt

As you can see the new file you created in the other branch has
disappeared. Not to worry, it is safely tucked away, and will re-appear
when you switch back to that branch.

Now, switch back to the branch your created with your name, and check that the `test.txt` is
now present.

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)
Stuck? Ask for help from the workshop staff

Merging
-------

We now try out merging. Eventually you will want to merge two branches
together after the conclusion of work.
`git merge` allows you to do that.

Git merging works by first switching the branch you want to *into*, and
then running the command to merge the other branch in.

We now want to merge our `jeroen-egelmeers` (but then your own) branch into `develop`. First, switch to
the `develop` branch.

    git checkout develop

Next, we merge the `jeroen-egelmeers` branch into `develop` :

    $ git merge jeroen-egelmeers

Do you see the following output ?

    Merge made by recursive.
     test.txt |    1 +
     1 files changed, 1 insertions(+), 0 deletions(-)
     create mode 100644 test.txt

You have to be in the branch you want to merge *into* and then you always
specify the branch you want to merge.

At this point, you can also try out `gitk` to visualize the changes and
how the two branches have merged

Pull Request
-------
In modern development, we work with Pull Requests. Here you can ask your peers to review your code. Let's try that out in Github!

- Create a new branch with again your name, but then add `-PR` after it. So for example:
  `jeroen-egelmeers-PR`

Do you still remember how to create the branch? If not, scroll back up, and find the solution!

- Now create a file called `my-favorite-mysic.txt`, add your top 3 favorite music numbers to it.
- Stage the files using the staging command.
- Commit the files using the commit command and don't forget the message. This way you let others know why you did this commit!
- Push your committed changes using:


    git push

Probably you got an error now. You did not yet create the branch on the online repostiroy, but only local.
Git gives an error message stating how to fix your issue. Can you figure it out yourself?

Now go to our online repository on Github using this link:
`https://github.com/JeroenEgelmeers/git-workshop`

- Click on the `Pull Request` tab.
- Click on the green button `New pull request`
- Now you see two boxes, "base: {branch-name}" and "compare: {branch-name}"
    - Click on the `compare` box, and select your branch.
    - Make sure the base is on `develop`
- Now there will be a new button `Create pull request` click on it to open your Pull Request.

Now you can edit your Pull Request. Github has an option to create "draft" Pull Requests. This is following the early pull request strategy which was explained to you during the presentaiton.
It's helpfull to get feedback along the way. But in some repostiries (such as Bitbucket) this feature is not available. In this case you could change the title, and put "WIP" or "DRAFT" in front of it. This way others know, you're still working on it.
Let's just create a Draft Pull Request and change nothing in the title or textbox. You can simple click on the arrow next to the green button "Create pull request".

If you click on the arrow, the option for a "Draft Pull Request" will be shown.
- Click on "Draft pull request"
- The button now will change to "Draft pull request". Click on it. 

Well done! Your draft pull request was created!

As soon as you're done with your code, and it can be set to the "Pull Request" status (and thus is ready to merge), click on the "Ready for review" button in your screen.
Let's do that!
- Click on the "Ready for review" button
- If nothing is wrong, and there are no merge conflicts, you should now have a button "Merge pull request". If you click that button, your changes will be merged to develop. But the repository you're using has rules. You need atleast one reviewer to accept your changes. Ask the workshop crew to review your branch to continue.
- When accepted, merge your PR!

Congratulations! You have worked yourself through you very first Pull Request!

You're fast! Here are some extra things to try!
---------------

Merge Conflicts
---------------

Git is pretty good at merging automagically, even when the same file is
edited. There are however, some situations where the same line of code
is edited there is no way a computer can figure out how to merge.
This will trigger a conflict which you will have to fix.

We now practise fixing merge conflicts. Recall that conflicts are caused
by merges which affect the same block of code.

Here’s a branch I prepared earlier. The branch is called `alpher`. Run
the code below to set it up (don’t worry if you can’t understand it)

    $ git checkout alpher

You should now have a new branch called `alpher`. Try merging that
branch into `develop` now and fix the ensuing conflict.

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)
Stuck? Ask for help from the workshop staff

Fixing a conflict
-----------------

You should see a `conflict` with the `alpher.txt` file. This means that
the same line of text was edited and committed on both the develop branch
and the alpher branch. The output below basically tells you the current
situation :

    Auto-merging alpher.txt
    CONFLICT (content): Merge conflict in alpher.txt
    Automatic merge failed; fix conflicts and then commit the result.

If you open the `alpher.txt` file, you will see something similar as
below:

    $ cat alpher.txt
    <<<<<<< HEAD
    Some changes
    =======

    Some other changes
    >>>>>>> alpher

Git uses pretty much standard conflict resolution markers. The top part
of the block, which is everything between `<<<<<< HEAD` and `======` is
what was in your current branch.
The bottom half is the version that is present from the `alpher` branch.
To resolve the conflict, you either choose one side or merge them as you
see fit.

For example, I might decide to choose the version from the `alpher`
branch.

Now, try to **fix the merge conflict**. Pick the text that you think is
better (Ask for help if stumped). You can also try using the Github Pull Request if you're stuck!
Github has nice options to edit in the webpage itself!

Once I have done that, I can then mark the conflict as fixed by using
`git add` and `git commit`.

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)
Stuck? Ask for help from the workshop staff

    $ git add alpher.txt
    $ git commit -m "Fixed conflict"

Congratulations. You have fixed the conflict. All is good in the world.

Congratulations! You've completed the workshop!
---

You have learnt :

1. How to install GIT
2. How to use Github (and set your security)
3. Clone a repository 
4. Commit files 
5. Check status 
6. Check diff 
7. Undoing changes 
8. Branching and merging 
9. Pull Requests (including WIP/DRAFT)
10. Fixing conflicts

Next time someone is asking you something about Git, you're ready to answer them! Congratulations!
Want to learn more? Try to create your very own repository, and start playing!

I wish you a wonderful day!

Create your first GitHub repository
-----------------------------------

A repository (repo) is a place where you would store your code. You were
practising on your very own repo just now in Part 1!

The following <a href="https://help.github.com/articles/create-a-repo">
tutorial</a> will show you how to create a GitHub repo - which you can
then share with others

Then come back here, we’ll wait.

Fork a repo
-----------

Go to [this tutorial](https://help.github.com/articles/fork-a-repo)
Then come back here, we’ll wait.

Fin
---

You have learnt:

1.  Forking a repo at GitHub
2.  Git push
3.  Git pull

### References and Further reading

I throughly recommend these resources to continue your Git practice:

-   <a href="http://try.github.com">http://try.github.com</a> Another
    beginners tutorial for git
-   <a href="http://git-scm.com">http://git-scm.com</a> Official
    website, with very useful help, book and videos
-   <a href="http://gitref.org">http://gitref.org</a>
-   <a href="http://www.kernel.org/pub/software/scm/git/docs/everyday.html">http://www.kernel.org/pub/software/scm/git/docs/everyday.html</a>

Author
------

This work is licensed under the Creative Commons
Attribution-NonCommercial-ShareAlike 3.0 License\
<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/3.0/">http://creativecommons.org/licenses/by-nc-sa/3.0/</a>\
Author: Thong Kuah
Contributors: Andy Newport, Nick Malcolm

Was editted for internal use by Jeroen Egelmeers
