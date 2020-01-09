# Contributing to $PROJECT

We would love for you to contribute to $PROJECT and help make it even better than it already is. This document provides some basic guidelines on how to make your first contribution.

 - [Question or Problem?](#question)
 - [Submission Guidelines](#submit)
 - [Coding Rules](#rules)
 - [Commit Message Guidelines](#commit)

## <a name="question"></a> Got a Question or Problem?

For general support requests please visit $PROJECT_CHANNEL on Slack. This channel is monitored by team members and developers and we'll try to address you concerns in a timely manner. Please refrain from using mechanisms such as `@here` and `@channel` to get the team's attention. If the team isn't responding right away, it's most likely that they're working together. We aim to provide responses to requests within 4 hours when submitted during normal working hours for the East Coast of the United States ([`America/New_York` tz entry](http://www.timezoneconverter.com/cgi-bin/zoneinfo?tz=America/New_York)). 

In addition, we have project office hours on Tuesdays from 11am-Noon in the `America/New_York` time zone. These are held in our standard Google Hangout room (INSERT LINK HERE). Please join the meeting with your headphones on and video enabled. If you have a complicated issue that you bring up over Slack, we may ask you to attend these office hours.

Before asking for help, we'd like you to collect a few pieces of information. This will help the team assist you with your problem much more quickly:

* If you have a specific question, do not say "Hi" and then wait for a response. You'll get the fastest response if you write a clear and concise question like "How do change the vendor name in the validator code?"

* If you have are seeking support, please clearly state the problem by saying something like "I'm getting a 503 error after using the current operator to deploy to my Kubernetes cluster." Then, be ready with the following pieces of information:
  - When did the error start?
  - Have you been able to reproduce the error?
  - Were there any changes that might've led to the error (e.g. switching versions)?
  - What have you already done to try and debug the error?

Under no circumstances should you take support requests to private messages, phone calls, or direct emails unless a member of the team asks you to. Doing those actions results in the solution being siloed away and prevents others from learning. The team will most likely redirect you to their Slack channel.

When you have resolved your issue, either on your own or with the help of team members, please revisit your thread and provide a comment to let the team and others know how it was resolved.

## <a name="coding-norms"></a> Coding Norms

We practice on this project we practice trunk based development with minimal merge commits. This creates a nice linear project history that makes it easy to follow who made what commit and for what reason.

Here is the general process for creating a patch for $PROJECT.

1. Fork the $ORGNAME/$PROJECT repo into your own account
1. Make your changes in a new git branch:

     ```shell
     git checkout -b fix/123-frobnicate-the-flux-capacitor
     ```

   The key here is that your git branch should have a clear and consistent name that includes the type of work, the issue that you're working against, and a brief description of the purpose of the branch. Clear and consistent naming will benefit your as much as it benefits us.

    In general, the naming scheme is as follows:

      `TYPE/ISSUENO-DESCRIPTION`

    Where `TYPE` is one of the types from our commit message format. Usually something like `fix`, `feat`, `docs,` etc. `ISSUENO` is the issue number from our tracker. `DESCRIPTION` is a brief description separated by underscores.

1. Create your patch, **including appropriate test cases**.
1. Commit your changes using a descriptive commit message that follows our
  [commit message conventions](#commit).

     ```shell
     git commit -a
     ```
    Note: the optional commit `-a` command line option will automatically "add" and "rm" edited files.
1. If you have multiple commits on your branch, [please squash those commits](https://blog.carbonfive.com/2017/08/28/always-squash-and-rebase-your-git-commits/) (this is sometimes called an interactive rebase). This can usually be done by running:

    ```shell
    git rebase -i HEAD~2
    ```

    Where you can replace the number 2 with the number of commits you need to look back and squash.
1. Push your branch to GitHub:

    ```shell
    git push origin fix/123-frobnicate-the-flux-capacitor
    ```

1. Send a pull request in GitHub against the master brnach.
* If we suggest changes then:
  * Make the required updates.
  * Squash back down to a signle commit
  * Rebase your branch and force push to your GitHub repository (this will update your Pull Request):

    ```shell
    git rebase master -i
    git rebase -i HEAD~2
    git push -f
    ```

That's it! Thank you for your contribution!

#### After your pull request is merged

After your pull request is merged, you can safely delete your branch and pull the changes
from the main (upstream) repository:

* Delete the remote branch on GitHub either through the GitHub web UI or your local shell as follows:

    ```shell
    git push origin --delete fix/123-frobnicate-the-flux-capacitor
    ```

* Check out the master branch:

    ```shell
    git checkout master -f
    ```

* Delete the local branch:

    ```shell
    git branch -D fix/123-frobnicate-the-flux-capacitor
    ```

* Update your master with the latest upstream version:

    ```shell
    git pull --ff upstream master
    ```

## <a name="commit"></a> Commit Message Guidelines

We have very precise rules over how our git commit messages can be formatted.  This leads to **more
readable messages** that are easy to follow when looking through the **project history**.  But also,
we use the git commit messages to **generate the Angular change log**.

### Commit Message Format
Each commit message consists of a **header**, **body**, **footer**, and **signoff**.  The header has a special
format that includes a **type**, a **scope** and a **subject**:

```
<type>(<scope>): <subject>
<BLANK LINE>
<body>
<BLANK LINE>
<footer>
<BLANK LINE>
<signoff>
```

The **header** is mandatory and the **scope** of the header is optional.

Any line of the commit message cannot be longer than 100 characters! This allows the message to be easier
to read on GitHub as well as in various git tools.

The footer should contain a [closing reference to an issue](https://help.github.com/articles/closing-issues-via-commit-messages/) if any.

The following are a couple of examples of reasonably well formatted commit messages:

```
docs(README): create initial README file

This is the initial project `README.md` file. It only includes contact information and a bit of a description about the current state of the project. In the future we should decide if it needs to include installation instructions too.

Closes #141

Signed-off-by: Joe Developer <joe.developer@example.com>
```

```
fix(docker): Correct dockerfile caching

The `Dockerfile` was broken up into too many steps and this resulted in many layers that didn't need to be cached. Thus, the image was huge. This combines most of hte 
fix(release): need to depend on latest rxjs and zone.js

The version in our package.json gets copied to the one we publish, and users need the latest of these.
```

### Revert
If the commit reverts a previous commit, it should begin with `revert: `, followed by the header of the reverted commit. In the body it should say: `This reverts commit <hash>.`, where the hash is the SHA of the commit being reverted.

### Type
Must be one of the following:

* **build**: Changes that affect the build system or external dependencies (example scopes: gulp, broccoli, npm)
* **ci**: Changes to our CI configuration files and scripts (example scopes: Circle, BrowserStack, SauceLabs)
* **docs**: Documentation only changes
* **feat**: A new feature
* **fix**: A bug fix
* **perf**: A code change that improves performance
* **refactor**: A code change that neither fixes a bug nor adds a feature
* **style**: Changes that do not affect the meaning of the code (white-space, formatting, missing semi-colons, etc)
* **test**: Adding missing tests or correcting existing tests

### Scope

The `scope` element is subjective and should be defined by the team and may differ based on the type. For example, `docs` may have scopes of `README`, `build`, and `installation` while `feat` may have scopes of `mobile`, `web`, `backend` or other. Over time these may need to become more specific.

### Subject
The subject contains a succinct description of the change:

* use the imperative, present tense: "change" not "changed" nor "changes"
* don't capitalize the first letter
* no dot (.) at the end

### Body
Just as in the **subject**, use the imperative, present tense: "change" not "changed" nor "changes".
The body should include the motivation for the change and contrast this with previous behavior.

**Breaking Changes** should start with the word `BREAKING CHANGE:` with a space or two newlines. The rest of the commit message is then used for this.

### Footer
The footer is a single line that references the GitHub issue that this commit closes. It should usually be succinct and read something like:

```
closes #123
```

In the even that the commit only partially addresses the issue, you may choose to write:

```
contributes to #123
```

## Sign-off

One of the down sides of doing pull requests and merging in code is that developer GPG signatures are usually lost. We still want to have a way to indicate who actually wrote what piece of code. That's where the sign-off comes into play.

The following statement will suffice:

```
Signed-off-by: YOUR NAME <your.name@email.com>
```

When you're signing off on a commit that's indicating that you, as the person at the email address, wrote the code for the commit. It's not quite as good as GPG signing, especially since git histories can still be manipulated, but it works well enough.

There may times that you want to commit code that you did not write. In those events, make a note of it in the sign-off block:

```
No sign off because this patch was submitted via email by l33th4x0r@phishing.com
```