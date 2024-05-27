# Git (and Hub) Tutorial

## [Why Git?](https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3F)

Git is a tool for file documenting. With Git, we can take snapshots of a file state and only store it if changes are made. This is very appealing for when you need to work with a lot of people, every change is documented and you can describe what you did. This helps when the team needs to find a bug, or human error.

Furthermore, Git is open source, this means that anybody can contribute with the code. Git itself doesn't need a host, but it's common to use [GitHub](github.com) or [GitLab](https://about.gitlab.com/). For this tutorial, we are going to mostly talk about GitHub.

## Some Git language

* **Clone** - Download hosted repository to your designated machine.
* **add** - Trace the changes you made.
* **commit** - Save the changes in Git.
* **push** - Upload your commits to a host.
* **pull** - Download commits from host to your designated machine (oposite of push).
* **Branch** - Some version of the repository.

## Installing Git

You can check how to download Git in the [official website](https://git-scm.com/downloads). But if you are using a Linux distro, you may write the following commands on the terminal:
```
sudo apt update
```
```
sudo apt install git
```
You may check it with
```
git --version
```

## Observations

When working with Git, you may be asked to confirm your user and password as it follows:

```console
Cloning into 'repository-example'...
Username for 'https://github.com': user-example
Password for 'https://user-example@github.com':
```

However, since 2021, GitHub has [stopped using passwords](https://dev.to/shafia/support-for-password-authentication-was-removed-please-use-a-personal-access-token-instead-4nbk#:~:text=Please%20use%20a%20personal%20access%20token%20instead.,-While%20pushing%20some&text=Starting%20from%20August%2013%2C%202021,follow%20the%20steps%20outlined%20below.) when the user is working with a repository.

Instead of writing your GitHub password in `Password for 'https://user-example@github.com':`, you will need a **Personal access token** and the steps to retrieve one are:

1. Settings;
2. Developer settings;
3. Personal access tokens;
4. Tokens (classic);
5. Generate new token (classic).

You may give it a name, change its expiration from 30 days to "No expiration" and check all boxes or check accoarding to your needed uses. 

**BE WARE: don't ever give your token to other people and write it down, you can't retrieve it after generating it.**

> **personal note from author**: I use [Bitwarden](https://bitwarden.com/) to store my token and you may use this or other password manager to do the same. When working with a lot of repositories it may be helpful to have easy access to your token. Just be careful and be sure that you can trust where you are storing this kind of information.

## Clone

To clone a GitHub repository, you need to Clone it with a link. This may be achieved by accessing your desired repository, clicking `<> Code` and copying the shown link.

For demonstration purposes, let's use our `repository-example` and clone it to our local machine:

```
git clone https://github.com/example-user/repository-example.git
```
And the output may be something like this:
```console
Cloning into 'repository-example'...
Username for 'https://github.com': user-example
Password for 'https://user-example@github.com': <token>
remote: Enumerating objects: 8499, done.
remote: Counting objects: 100% (1183/1183), done.
remote: Compressing objects: 100% (483/483), done.
remote: Total 8499 (delta 757), reused 1021 (delta 646), pack-reused 7316
Receiving objects: 100% (8499/8499), 65.14 MiB | 9.64 MiB/s, done.
Resolving deltas: 100% (5731/5731), done.
```
Sometimes the repository doesn't ask for a user and password (token) input, it's up to the author's.

To enter the repository:
```
cd repository-example
```
And depending on the terminal you are using, it's possible to have some indication that you are in a git enviroment, just like below:
```console
user-example@user-computer repository-example git:(master)
```
> **personal note from author**: I use [Warp terminal](https://www.warp.dev/), it's very new but it's also beautiful! Really recommend it.

## Commit

Now, let's create an `tutorials` folder so that co-workers may write tutorials for new people in our group!
```
mkdir tutorials
```
And now, we can `add` to track our changes:
```
git add .
```
The `.` tells git that we want to track all the changes we made! And now, we may commit our work explaining what we've done.
```
git commit -m "Created a tutorials folder so that the team can create tutorials for new people in the group."
```

## Push

Now, if we want to edit the `master` branch, we need to `git push` our changes:
```
git push master
```
`master` is the branch we want to edit.

## Branches

The most powerful tool of Git is its branching capabilities, anyone can create a new Branch using another one as a base. So, for example, a co-worker added a wrong command on a python tutorial in the `tutorials` folder and you need to find it. The easiest way to do so is to test all commands and comment if it's right or wrong.

So firts, let's check out which branches are available:
```
git branch --list
```
```console
* master
python-tutorial
cpp-tutorial
git-tutorial
```
We can then change to the `python-tutorial` branch
```
git checkout python-tutorial
```
And as you don't want to affect your co-worker's work, we can create a new branch:
```
git branch python-tutorial-debug
```
And now you are able to change anything without altering your co-worker's work.

Before merging both branches you may want to check the differences between both:
```
git diff python-tutorial python-tutorial-debug
```
If everything is fine, you may proceed to `git add`, `git commit`, `git push` as usual and then `git merge`:
```
git checkout python-tutorial
```
```
git merge python-tutorial-debug
```
This merges the `python-tutorial-debug` branch on top of the `python-tutorial` one.
