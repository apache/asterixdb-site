---
title: Contributing to AsterixDB
---

---

* Table of Contents
{:toc}


---

## Introduction
We warmly welcome any contributions to the Apache AsterixDB&trade; or related (Hyracks, Pregelix) projects.
A great way to start contributing is to pick a bug labelled starter in JIRA and submit a patch for it, to get acquainted with our codebase and development process.

---

## Master snapshots
If you are a developer simply looking for a snapshot of the latest development version of AsterixDB to test out your application that is based on top of AsterixDB, snapshots from the latest successful push to our master branch are available below. These are non ASF-release, automatic builds.

### Server Package
<p><a class="btn btn-md btn-warning" href="{{ site.UNSTABLE_NCSERVICE_URL }}" role="button">Download AsterixDB Dev Build <i class="fa fa-download fa-lg"></i> </a></p>

---

## Setting up an Asterix Development environment

### Prerequisites
  * A suitable \*nix environment (Linux, OSX)
  * JDK 1.8+
  * Maven 3.3.9 or greater
  * Eclipse Juno (or later) or IntelliJ IDEA 15.0 (or later)

### Steps

#### General setup

1. Check out AsterixDB master in one folder via git in the command line. Assume that the path is `$HOME/workspace`.

        git clone https://github.com/apache/asterixdb/

    You will now have `$HOME/workspace/asterixdb/`.

2. Go to the asterixdb folder and install it's artifacts to the local Maven repository by executing the following commands:

        cd asterixdb/
        mvn install -DskipTests

#### IntelliJ IDEA IDE Setup


3. In IntelliJ IDEA, import asterixdb as an existing Maven Project.
* `File -> New -> Project from existing sources`, or `Import project...' when on a new install
* Then, select the 'pom.xml' in the root of the checked out git repository.
* The default options for import should suffice, so just click `Next`
* Also click `Next` when selecting for profiles and versions
* On the JDK Selection screen, be sure to select a JDK > 1.8, OpenJDK or Oracle is fine.
* Give IntelliJ some time to import the Maven project and its dependencies
* Once everything is finished, you should see 'asterixdb' and 'hyracks-fullstack' modules in the "Project" view.

4. Set up IntelliJ code formatting rules
* Download files [AsterixCodeFormatProfile.xml](https://cwiki.apache.org/confluence/download/attachments/61322291/AsterixCodeFormatProfile.xml)
    [AsterixCleanupFormatProfile.xml](https://cwiki.apache.org/confluence/download/attachments/61322291/AsterixCleanupFormatProfile.xml)
* Import profiles into IntelliJ
    * `File -> Settings -> Editor -> Code Style -> Java`
    * Then, click the `Manage...` button
    * Click `Import` and import the `AsterixCodeFormatProfile.xml` as an Eclipse XML profile.

#### Eclipse IDE Setup

3. In Eclipse, import asterixdb as an existing Maven Project.
  * `File -> Import -> Maven -> Existing Maven Projects -> Next`
  * Specify the Root directory as `asterixdb` and then click Next until Finish is enabled.
  * If Eclipse tries to install the `m2e` (Maven To Eclipse) connector, let it do so.
  * There might be some plugin errors; however, that is not a big deal. Wait until the job finishes.
  * Then, click Finish. Restart Eclipse if asked to do so.

4. Fix Eclipse's build path to include compile-time generated sources.
  * Right click the project where a red X mark is shown(e.g. `asterix-algebra`. Then resolve by applying the following:
       * Right click asterix-algebra. Click Build Path and Configure Build Path. Click Add Folder.
       * Under the `target -> generated sources`, check the parent folder of the `org` folder and click OK.
       * For example, if the directory structure is "target - generated-sources - javacc - org - apache ...", check the javacc directory and click OK. Then X mark will dissapear.
  * Repeat this step to all projects which show a red X mark except "asterix-fuzzyjoin" and "asterix-transactions".
  * It may be the case that only "asterix-algebra" and "asterix-external-data" will require these steps.
  * If you see "plugin execution not covered by lifecycle configuration" errors such as this one - "Plugin execution not covered by lifecycle configuration: org.apache.asterix:asterix-test-datagenerator-maven-plugin:0.8.9-SNAPSHOT:generate-testdata (execution: replace-template-data, phase: process-test-resources)", try to resolve it using the quick fix feature. You can call this feature by right click on the error and select "quick fix". And then choose "Mark goal generate-testdata as ignored in Eclipse build in Eclipse preferences".

5. Set up Eclipse code formatting rules
  * Download files [AsterixCodeFormatProfile.xml](https://cwiki.apache.org/confluence/download/attachments/61322291/AsterixCodeFormatProfile.xml)
      [AsterixCleanupFormatProfile.xml](https://cwiki.apache.org/confluence/download/attachments/61322291/AsterixCleanupFormatProfile.xml)
  * Import profiles into Eclipse
       * Preferences -> Java -> Code style -> Formatter -> Import -> Select AsterixCodeFormatProfile.xml
       * Preferences -> Java -> Code style -> Clean up -> Import -> Select AsterixCleanupFormatProfile.xml
       * Preferences -> Java -> Editor -> Save actions -> Perform the selected action on save -> Format source code

6. Lastly, go to the asterixdb folder and execute following command again. This is required since Eclipse might have cleaned the projects and rebuilt the them without creating all necessary classes. Currently, some of the class files can be only built using mvn command.

        cd asterixdb/
        mvn install -DskipTests

---

## Signing Up for Gerrit

First, to contribute patches to AsterixDB, you should have an ICLA on file with the Apache Software Foundation.
For details see the ASF website [here](https://www.apache.org/dev/new-committers-guide.html#cla)
You should only need to perform the following steps once.

Our Gerrit server is [here](https://asterix-gerrit.ics.uci.edu/)

  1. Visit the above URL, and click on "Register" in the upper right.
  1. Gerrit uses OpenID; you may create an account using any OpenID provider, or with a Yahoo! account.
  1. Click on "Sign in with a Yahoo! ID". You will be taken to a page to log in to Yahoo!.
  1. From there, you will get a page asking you to allow `asterix-gerrit.ics.uci.edu` to access your email and basic information.  Approve this request.
  1. You will be directed back to Gerrit to complete the account signup. Make sure to fill out this page! It is necessary to allow you to push code changes to Gerrit for review.
  1. For "Full Name" and "Preferred Email", enter what you like. If you would like to register a different email address such as an @uci.edu address, you may do so. This is where Gerrit will send you notifications about code review requests, voting, and so on.
  1. For "Select a unique username", choose a short alphanumeric ID. This will be your ssh username for git access. Be sure to click "Select Username" to verify that the name is unique and allowed.
  1. Also provide a ssh public key here. There is information on the page on creating one if you do not have one. Click "Add" when done.
     Note that you can create a new ssh public key just for Gerrit if you like; if you do so you will need to modify your `.ssh/config` file to ensure the right key is selected.
  1. Click "Continue" at the bottom of the page.
  1. Finally, verify that you have everything set up: From a command-line, type

         ssh -p 29418 username@asterix-gerrit.ics.uci.edu

  1. You should see

         ****    Welcome to Gerrit Code Review    ****

         Hi Full Name, you have successfully connected over SSH.

         Unfortunately, interactive shells are disabled.
         To clone a hosted Git repository, use:

         git clone ssh://username@asterix-gerrit.ics.uci.edu:29418/REPOSITORY_NAME.git

At this point, please send an email to Chris or Ian, specifying the email address of your new account, and ask to be added to the "AsterixDB Devs" group. You may push change proposals to Gerrit, and vote +1/-1 Code Review on any proposals without being in AsterixDB Devs, but you cannot vote +2 on anything to allow a change to be merged.

---

## Configuring your local working environment for Gerrit

### One-time tasks

  1. At the command-line, run the following. Replace "username" with the user name you chose in step 7 above.

         git config --global gerrit.url ssh://username@asterix-gerrit.ics.uci.edu:29418/

  1. Download my "git-gerrit" utility library:

         git clone https://github.com/ceejatec/git-gerrit

  1. Ensure that the `git-gerrit/git-gerrit` script is on your PATH. You could copy it to somewhere, but it would be best to leave it inside the github clone so you can easily get updates.

### Once-per-repository tasks

  1. To work on (say) Asterix, first clone the GitHub mirror or the ASF repository (if you already have a local clone, great!), e.g.

         git clone https://github.com/apache/asterixdb

  1. `cd` into the clone repo directory, and then run the following command to create the "gerrit" remote.

         git gerrit init


---

## Making Changes - working method

  1. When you want to start working on a bug, feature, etc, first make a local `git` branch. Never work directly on
    `master`! `master` should always be a pure mirror of `origin/master`, i.e., the GitHub mirror or the ASF repository.

         git checkout -b my_branch

  1. Make your changes, test them, etc. Feel free to `git commit` as often as you like.

  1. **Optional**: If you like, you can push your branch up to another git repository (e.g. in your own GitHub account), either to share it with others or as a backup. You may do this at whatever point in time you like.

  1. Every so often, you should update your local `master` mirror, and then merge that onto your working branch. This will prevent your branch from falling too far out of date, and ensure that your code review proposals will merge successfully with `master`. There are a number of ways to do this, but `git-gerrit` provides a convenience function:

         git gerrit update

  1. When you are ready to submit changes for code review, first ensure that you have committed everything locally that is necessary (`git status` should report "nothing to commit, working directory clean"). This is also a good time to update (see step 4). Then run:

         git gerrit submit

  1. This will pop open your editor to invite you to create a good commit message. This will be the single commit message which will be the only one to appear in the project's master git history. Take the time to make it clear. The editor will contain the log messages of everything you committed on your branch as a reminder, but generally you will want to delete all this and replace it with a comprehensive message. Also: As noted in the initial message, the last line of the buffer will contain a `Change-Id` field. Do not delete that line! It is used by Gerrit to identify this particular merge proposal.
  1. When you save your commit message, git-gerrit will push all of the changes from your working branch up to Gerrit. Assuming no errors, you should see output similar to the following:

         remote: Resolving deltas: 100% (1/1)
         remote: Processing changes: new: 1, refs: 1, done
         remote:
         remote: New Changes:
         remote:   http://fulliautomatix.ics.uci.edu:8443/30
         remote:
         To ssh://ceej@fulliautomatix.ics.uci.edu:29418/ceej-gerrit-test
          * [new branch]      HEAD -> refs/for/master

  1. That URL under "New Changes" is your code review! Send it to others to request reviews.
  1. If you get any negative code reviews and need to make changes, you can just repeat steps 2 - 6 of the working method. Your local branch will still have all the history you put there, if you need to revert changes or look back and see what you did, etc.
  1. When you repeat step 6, you will notice two things: First, git-gerrit keeps the change message for you, including the Change-Id, so you don't have to re-invent it every time. Second, the output from `git gerrit submit` will not include the URL of the review this time. I'm not sure why; I wish it did. But if you re-visit the old URL in your browser, you should see an additional "Patch Set" containing your revised changes for people to review.

## Making More Changes

You may have as many feature branches as you want locally, and each may be at any point in the review cycle.

Once you are done with a change (that is, it has been Code Reviewed and approved in Gerrit and merged), it is probably best to start work on the next big thing on a new branch. However, git-gerrit attempts to be smart if you choose to re-use a branch. For example, it should notice if the "current" Change-Id for a branch has been merged to master, and it will create a new Change-Id and a new fresh commit message the next time you run `git gerrit submit`.

In that case, you may notice that the list of changes on the branch still contains older commits which have been merged. That is due to the unfortunate way Gerrit works; it requires squashing to a single git commit for review, which loses the association with the original commits in your history.

It is also possible that you may want to re-use a branch and git-gerrit fails to notice that the older change has been merged - or perhaps the change was Abandoned on Gerrit and not merged, and you want to continue working on the same branch to create a new proposal. In this case, run

    git gerrit new

on your branch. This will force git-gerrit to create a new Change-Id and commit message the next time you run `git gerrit submit`.

---

## Using Jenkins with Gerrit

### Verification

As of right now, whenever a patch set is submitted to Gerrit (i.e. whenever a user performs 'git gerrit submit') are automatically picked up by Jenkins, which runs `mvn verify` to test the patch fully.
Once the build finishes, Jenkins comments on the patchset and votes with the result (+1 for all tests passing, -1 for anything less).
Ideally, and in most cases, verification of a patchset reqires no intervention.
However there are a few exceptions to this as detailed below.

### Retrigggering builds and triggering builds manually

#### Retriggering
Occasionally, there are builds in which tests failed, but perhaps not for a reason that has anything to do with the proposed patch's changes.
For example, on occasion the Integration tests can have issues with ports on the build server already being bound.
The simple work around to this is to try building again.

One way to perform this is by simply visiting the link that is posted on Gerrit by Jenkins, and hitting the 'Retrigger' link on the left-hand side of the page.
This will try retesting the build with the exact same parameters as last time, hopefully with a different result.

#### Manual Trigger
Builds of Gerrit patches can also be fully manually triggered from Jenkins.
This can be desirable if the patch is a draft or is not triggered automatically for any other reason.
To manually trigger a build of a patchset, visit the Jenkins front-page, and click the 'Query and Trigger Gerrit patches' link.
This should link to a page allowing you to manually trigger Gerrit patches.
In the search field any query that can be searched in the Gerrit web interface can be used, but the default query of all open patchsets is likely fine.
Hit the 'Search' button, and then click the checkbox that represents the patch that needs to be built.
Then simply click 'Trigger Selected' and the patch will start building.

---
