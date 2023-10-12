# Jenkins CI Task

![AltText](Images/diagram.png)

Our current CI setup on Jenkins has one major flaw. The build is currently started and the tests are run on the main branch of the repository. This means that if the tests fail the code still exists on the main branch (which is only supposed to contain working code).

We need to reconfigure the job so that the code is tested on a different branch (dev) and automatically merged with the main branch if the tests pass.

<br>

### Tasks:

1. Configure your job to checkout code from the dev branch rather than the main branch.

![AltText](Images/branch.png)


2. Have the job merge the dev branch code with the main branch and test against that.

Changing the settings in the first job (irina-CI) to run the second job of **merging branches** (irina-merge) only if the Build is stable:

![AltText](Images/post_build.png)

3. Use the Git publisher plugin to push the main branch to Github if the tests pass.

**a.** Changing Configuration in the *Merge Job* to merge branches: 

![AltText](Images/additional.png)

**b.** In Git Publisher, ticking the box to "Merge Results" and "Branches to push":

![AltText](Images/git_publisher.png)

**c.** Add SSH credentials:

![AltText](Images/credentials_ssh.png)

**d.** After a push to the "dev" branch of the repo, the 2 jobs will run and both 'main' and 'dev' branches will be updated on GitHub:

![AltText](Images/github_branches.png)


<br>

Sources: 

[Jenkins Git Merges](https://andrewtarry.com/posts/jenkins_git_merges/)