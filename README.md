# cs580s2020 project-proposal

Designed for use with [GitHub Classroom](https://classroom.github.com/), this
repository contains starter files for the proposal project in CMPSC 580 Spring 2020.
Since the Travis builds for this repository will initially fail
(as evidenced by a red &#x2717; appearing in the commit logs instead of a green
&#x2714;), the programmer is responsible for completing all of the steps needed
to satisfy the requirements for the assignment, thus causing a &#x2714; to
instead appear in the commit logs.

## Introduction

The source code for all of the LaTeX source code files must adhere to all of the requirements in the
[Overleaf LaTeX Style Guide](https://www.overleaf.com/learn/latex/Style_Guide).
The source code in the submitted LaTeX source code files must also pass
additional tests set by the [GatorGrader
tool](https://github.com/gatored/gatorgrader).

When you use the `git commit` command to transfer your source code to your
GitHub repository, [Travis CI](https://travis-ci.com/) will initialize a build
of your assignment, checking to see if it meets all of the minimum requirements. If both
your commit meets all of the established requirements, then you
will see a green &#x2714; in the listing of commits in GitHub. If your
submission does not meet the requirements, a red &#x2717; will appear instead.
The instructor will reduce a student's grade for this assignment if the red
&#x2717; appears on the last commit in GitHub immediately before the
assignment's due date.

A carefully formatted assignment sheet for this project provides more details
about the steps that a computer scientist should take to complete this
assignment. You can view this assignment sheet by visiting the listing of
laboratories on the course web site.

Your course instructor will reduce a researcher's grade for this assignment if
the pdf of your completed proposal document has not been properly released before the
assignment's due date. Unless
you provide the course instructor with documentation of the extenuating
circumstances that you are facing, no late work will be considered towards your
grade for this project.

## Travis

This assignment uses [Travis CI](https://travis-ci.com/) to automatically run
the checking programs every time you commit to your GitHub repository. The
checking will start as soon as you have accepted the assignment, thus creating
your own private repository, and the course instructor enables Travis for it. If
you are using Travis for the first time, you will need to authorize Travis CI to
access the private repositories that you created on GitHub. You will partially
complete this authorization by following intuitive steps in your web browser.
You will also need to type the command `travis login --pro` in your terminal
window when you are in the root of your GitHub repository.

## Security

In order for Travis to automatically upload a PDF of your proposal template
 to GitHub when you tag the commit, you need to
created your encrypted access token. To complete this task,
in your GitHub repository for this assignment, you must type the
command:

`travis setup releases --com --force`

Then, when prompted, please type your username and password for
GitHub. When asked to give the filename, you can type:

`_build/senior_thesis_proposal.pdf`.

When asked if you want to deploy from a
specific repository, you can respond with the answer of "no". Finally, when
this tool asks if you want to use encryption, please answer with a "yes".

Now, you should have a `.travis.yml` file with a secure access token for your
GitHub repository for this assignment. Use a text editor to edit this file and
place the following lines of code at the bottom of it. Please note that you must
preserve the spacing in the following code segment when you paste it into your
own `.travis.yml` file. Now, you should be ready to perform a commit with tags
and see your PDF uploaded to GitHub!

```
  skip_cleanup: true
  on:
    tags: true
```

## Tagging

Since this repository primarily contains LaTeX source code, the Travis CI
configuration for it will compile the source code and automatically release a
PDF of the main file whenever the last commit is associated with a [Git
Tag](https://git-scm.com/book/en/v2/Git-Basics-Tagging). As such, this will
cause a PDF file to become available in the listing of the "Releases" listing
for this repository. All release numbers for your writing in this repository
should adhere to the [Semantic Versioning](http://semver.org/) standard that
all GitHub projects are asked to adopt.

Please note that the instructor and the technical leaders will only read the PDF
by downloading the "tagged" release of the proposal that has a version number greater than
1.0.0. That is, if your commit is tagged with
`SeniorThesisProposal-jjumadinova-1.0.0`, then the file
`SeniorThesisProposal.pdf` should be available for download in the
"Releases" tab in your GitHub repository for this project under the name
`SeniorThesisProposal-jjumadinova-1.0.0`.

Once you have finished making  small changes to the
document, you should commit your file using a `git
commit` command. Now, to create your first tag for this repository you could
type `git tag SeniorThesisProposal-jjumadinova-0.1.0`. Of course, you should
substitute your user name for `jjumadinova` when you create the tag. At this point,
you are ready to push your changes with the appropriate tag by typing the
command `git push -u origin master --tags`. After waiting for a period of time,
you should see that your GitHub repository features a new release of the
document that you must create for this project.

When you make subsequent changes to your files and perform commits and you are
ready to release a new version of `senior_thesis_proposal.pdf`, then you should
again tag your work &mdash; before running a push &mdash; with a tag that
adheres to the [Semantic Versioning](http://semver.org/) standard. Each time
that you correctly execute this sequence of commands you will release a new
version of your document to GitHub that is easily accessible as a PDF to you and
to your first and second readers. If you are unable to create a tagged release
using the automated system that Travis provides you can manually create one by
using GitHub's web interface; to adopt the manual approach please click the
"Draft a new release" button in the Releases tab of your GitHub repository.

### Using Docker and GatorGrader

Once you have installed [Docker
Desktop](https://www.docker.com/products/docker-desktop), you can use the
following `docker run` command to start `gradle grade` as a containerized
application, using the [DockaGator](https://github.com/GatorEducator/dockagator)
Docker image available on
[DockerHub](https://cloud.docker.com/u/gatoreducator/repository/docker/gatoreducator/dockagator).

```bash
docker run --rm --name dockagator \
  -v "$(pwd)":/project \
  -v "$HOME/.dockagator":/root/.local/share \
  gatoreducator/dockagator
```

This command will use `"$(pwd)"` (i.e., the current directory) as
the project directory and `"$HOME/.dockagator"` as the cached GatorGrader
directory. Please note that both of these directories must exist, although only
the project directory must contain something. Generally, the project directory
should contain the source code and technical writing of this assignment, as
provided to a student through GitHub. Additionally, the cache directory should
not contain anything other than directories and programs created by DockaGator,
thus ensuring that they are not otherwise overwritten during the completion of
the assignment. To ensure that the previous command will work correctly, you
should create the cache directory by running the command `mkdir
$HOME/.dockagator`. If the above `docker run` command does not work correctly on
the Windows operating system, you may need to instead run the following command
to work around limitations in the terminal window:

```bash
docker run --rm --name dockagator \
  -v "$(pwd):/project" \
  -v "$HOME/.dockagator:/root/.local/share" \
  gatoreducator/dockagator
```

Since the above `docker run` command uses a Docker images that, by default, runs
`gradle grade` and then exits the Docker container, you may want to instead run
the following command so that you enter an "interactive terminal" that will
allow you to repeatedly run commands within the Docker container.

```bash
docker run -it --rm --name dockagator \
  -v "$(pwd)":/project \
  -v "$HOME/.dockagator":/root/.local/share \
  gatoreducator/dockagator /bin/bash
```

Once you have typed this command, you can use the [GatorGrader
tool](https://github.com/GatorEducator/gatorgrader) in the Docker container by
typing the command `gradle grade` in your terminal. Running this command will
produce a lot of output that you should carefully inspect. If GatorGrader's
output shows that there are no mistakes in the assignment, then your source code
and writing are passing all of the automated baseline checks. However, if the
output indicates that there are mistakes, then you will need to understand what
they are and then try to fix them.

Here are some additional commands that you may need to run when using Docker:

* `docker info`: display information about how Docker runs on your workstation
* `docker images`: show the Docker images installed on your workstation
* `docker container list`: list the active images running on your workstation
* `docker system prune`: remove many types of "dangling" components from your workstation
* `docker image prune`: remove all "dangling" docker images from your workstation
* `docker container prune`: remove all stopped docker containers from your workstation
* `docker container stop ID`: stop the running container with specified ID
* `docker rmi $(docker images -q) --force`: remove all docker images from your workstation

## Assistance

If you are having trouble completing any part of this project, then please talk
with your instructor.
