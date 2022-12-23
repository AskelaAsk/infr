---
jupyter:
  colab:
  kernelspec:
    display_name: Python 3
    name: python3
  language_info:
    name: python
  nbformat: 4
  nbformat_minor: 0
---

::: {.cell .markdown id="VHdGmDRFnxwF"}
# 1 - Dependencies management {#1---dependencies-management}

***git branch name:*** dependencies
:::

::: {.cell .markdown id="mt6SsP_Ev4DQ"}
## Theory \[2\]

As usual, we will start with a few theoretical questions:

-   \[0.5\] What is Docker, and how it differs from dependencies
    management systems? From virtual machines?
-   \[0.5\] What are the advantages and disadvantages of using
    containers over other approaches?
-   \[0.5\] Explain how Docker works: what are Dockerfiles, how are
    containers created, and how are they run and destroyed?
-   \[0.25\] Name and describe at least one Docker competitor (i.e., a
    tool based on the same containerization technology).
-   \[0.25\] What is conda? How it differs from apt, yarn, and others?
:::

::: {.cell .markdown id="Tse_vanOXt9R"}
-   \[0.5\] What is Docker and how does it differ from dependency
    management systems? From virtual machines?

Docker is an open source platform for creating, deploying, and managing
container applications.

Docker differs from other dependency management systems in its
flexibility and security. Also, this cloud server provides many free
applications, as well as many public and private registries with
official repositories from leading third---party vendors - from Nginx
and Ubuntu to MongoDB and Redis.

Docker is designed to be lightweight and simple. It has a good security
level of 760 and is very popular to use, so if you find a bug, the
probability that you will find a solution online is 99%.

While every workload on a virtual machine (VM) requires a full-fledged
OS or hypervisor, many workloads can run on a single OS when using
Docker.

Docker containers have a fast startup time and reduce loading time.
Running virtual machines takes some time and has terrible performance.
Since Docker containers are smaller than virtual machines, it is easier
to move files to the host file system.

Due to the fact that the OS is running, Docker containers applications
start immediately. Virtual machines must run a full operating system to
install a single program, which requires a full boot process.
:::

::: {.cell .markdown id="FaJFELvvXt9V"}
-   \[0.5\] **What are the advantages and disadvantages of using
    containers over other approaches?**

Benefits of containers.

Containers are a streamlined way to build, test, deploy, and redeploy
applications on multiple environments from a developer's local laptop to
an on-premises data center and even the cloud. Benefits of containers
include:

*Less overhead*

Containers require less system resources than traditional or hardware
virtual machine environments because they don't include operating system
images.

*Increased portability*

Applications running in containers can be deployed easily to multiple
different operating systems and hardware platforms.

*More consistent operation*

DevOps teams know applications in containers will run the same,
regardless of where they are deployed.

*Greater efficiency*

Containers allow applications to be more rapidly deployed, patched, or
scaled.

*Better application development*

Containers support agile and DevOps efforts to accelerate development,
test, and production cycles.

Containers vs. virtual machines (VMs) People sometimes confuse container
technology with virtual machines (VMs) or server virtualization
technology. Although there are some basic similarities, containers are
very different from VMs.

Virtual machines run in a hypervisor environment where each virtual
machine must include its own guest operating system inside it, along
with its related binaries, libraries, and application files. This
consumes a large amount of system resources and overhead, especially
when multiple VMs are running on the same physical server, each with its
own guest OS.

In contrast, each container shares the same host OS or system kernel and
is much lighter in size, often only megabytes. This often means a
container might take just seconds to start (versus the gigabytes and
minutes required for a typical VM).
:::

::: {.cell .markdown id="7qVZHBWAXt9W"}
-   \[0.5\] Explain how Docker works: what are Dockerfiles, how are
    containers created, and how are they run and destroyed?

**Dockerfile**

Dockerfile is a text document that contains all the commands a user
could call on the command line to assemble an image.

**Сreate a directory in order to store all the Docker images that will
be builded**

    mkdir docker_dir_name #create a directory
    cd docker_dir_name  #move to it
    touch Dockerfile
    nano Dockerfile #open the file in text editor

Then, add the following content:

    FROM ubuntu
    MAINTAINER author
    RUN apt-get update
    CMD ["echo", "Welcome to the container"]

ctrl+C, ctrl+X

**Build a Docker Image with Dockerfile**

    docker build [OPTIONS] PATH | URL | - #declare the path where we will be storing the dockerfile docker_dir_name
    docker build [location of your dockerfile] #build a basic image using a Dockerfile
    docker build -t image_name #to make the new image be tagged with a name
    docker images #verify the creation

The output should show the image is available in the repository.

**Create a New Container**

    docker run [OPTIONS] IMAGE [COMMAND] [ARG...] #run a command in a new container (reates a writeable container layer over the specified image, and then starts it using the specified command.)

**Destroy it**

    docker kill [OPTIONS] CONTAINER [CONTAINER...] #kill one or more running containers (By default SIGKILL signal is sended but can be customized)
:::

::: {.cell .markdown id="Ues8VMp6Xt9W"}
-   \[0.25\] Name and describe at least one Docker competitor (i.e. a
    tool based on the same containerization technology).

**CoreOS Rkt**

A software containerization mechanism called CoreOS rkt (pronounced
\"rocket\") allows you to run application workloads separately from the
underlying infrastructure. This is the main competitor of the Docker
container engine.

The Application Container Image (ACI) from the application container
specification serves as the basis for CoreOS rkt (appc). ACI is an
archive consisting of an image manifest and a root file system with all
the files needed to run the application. Most of the default settings
can be changed at runtime, and the rkt run command allows users to add
their own execution parameters to a specific image.

Most major Linux OS versions support CoreOS rkt containers as a binary
file. Modules, which are sets of simultaneously running programs, are
used by CoreOS rkt to configure the container.

The module can include various configurations for various applications,
starting from the module level and ending with specific applications
within the module. The modules work independently and in remote
locations without a central daemon.
:::

::: {.cell .markdown id="Bxr8kOm7Xt9X"}
-   \[0.25\] What is conda? How does it differ from apt, yarn and
    others?

Conda is an open source package management system and environment
management system that runs on Windows, macOS, Linux and z/OS. Conda
quickly installs, launches and updates packages and their dependencies.
Conda easily creates, saves, downloads and switches between environments
on your local computer. It was created for Python programs, but it can
package and distribute software for any language.

Conda is more popular for the needs of developers (it has many developer
tools compared to yarn). This allows the user to work locally in
environments that are not in the root/bin directory, for example, the
user can use different versions of python in each environment (conda vs
apt).
:::

::: {.cell .markdown id="m--WCrL11SRM"}
## Problem \[6.5\] {#problem-65}

The problem itself is relatively simple.

Imagine that you developed an excellent RNA-seq analysis pipeline and
want to share it with the world. Based on your experience, you are
confident that the popularity of the pipeline will be proportional to
its ease of use. So, you decided to help your future users and to pack
all dependencies in a Conda environment and a Docker container.

Here is the list of tools and their versions that are used in your work:

-   [fastqc](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/),
    v0.11.9
-   [STAR](https://github.com/alexdobin/STAR), v2.7.10b
-   [samtools](https://github.com/samtools/samtools), v1.16.1
-   [picard](https://github.com/broadinstitute/picard), v2.27.5
-   [salmon](https://github.com/COMBINE-lab/salmon), commit tag 1.9.0
-   [bedtools](https://github.com/arq5x/bedtools2), v2.30.0
-   [multiqc](https://github.com/ewels/MultiQC), v1.13
:::

::: {.cell .markdown id="hehShsYn1Tv0"}
**Anaconda**:

-   \[1\] Install conda, create a new virtual environment, and install
    all necessary packages.
-   \[0.75\] You won\'t be able to install some tools - that\'s fine.
    List their names, and explain what should be done to make them
    conda-friendly
    ([conda-forge](https://conda-forge.org/docs/maintainer/adding_pkgs.html)
    channel,
    [bioconda](https://bioconda.github.io/contributor/workflow.html)
    channel).
-   \[0.25\]
    [Export](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#exporting-the-environment-yml-file)
    the environment
    ([example](https://github.com/nf-core/clipseq/blob/master/environment.yml))
    to the file and verify that it can be
    [rebuilt](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#creating-an-environment-from-an-environment-yml-file)
    from the file without problems.
:::

::: {.cell .code id="iOy-J3SoL7ma"}
``` {.python}
##Install conda
%%bash
MINICONDA_INSTALLER_SCRIPT=Miniconda3-4.5.4-Linux-x86_64.sh
MINICONDA_PREFIX=/usr/local
wget https://repo.continuum.io/miniconda/$MINICONDA_INSTALLER_SCRIPT
chmod +x $MINICONDA_INSTALLER_SCRIPT
./$MINICONDA_INSTALLER_SCRIPT -b -f -p $MINICONDA_PREFIX
```
:::

::: {.cell .code id="Az9CBXDQNF4E"}
``` {.python}
## Добавляю каналы Forge && Bioconda
%%bash
conda install --channel defaults conda python=3.9 --yes
conda update --channel defaults --all --yes
conda update -n base -c defaults conda
conda config --add channels defaults
conda config --add channels bioconda
conda config --add channels conda-forge
conda config --set channel_priority strict
```
:::

::: {.cell .code id="iXzuslBnNYYT"}
``` {.python}
## init conda env
%%bash
conda create --name hw_env python=3.9
conda activate hw_env
```
:::

::: {.cell .code id="XTA_3wTTNgIq"}
``` {.python}
# install conda packages
%%bash
conda install -y star=2.7.10b  
conda install -y samtools=1.16.1 
conda install -y bedtools=2.30.0 
conda install -y salmon=1.9.0
conda install -y fastqc=0.11.9
```
:::

::: {.cell .code id="Y0Vy_PPBN5VX"}
``` {.python}
!pip install multiqc
```
:::

::: {.cell .code id="DITSNBvcN0iz"}
``` {.python}
%%bash
git clone -b 2.27.5 https://github.com/broadinstitute/picard.git
cd picard
./gradlew shadowJar
java -jar build/libs/picard.jar
./gradlew clean 
```
:::

::: {.cell .code id="lM9G_DhfOGQu"}
``` {.python}
!conda env export > hw_env.yml  
```
:::

::: {.cell .markdown id="pWDOph3xL61u"}
**Docker**:

-   \[3\] Create a Dockerfile for a container with **all** required
    dependencies. Conda usage is not allowed, don\'t forget about
    comments; test that all tools are accessible and work inside the
    container. Hints:
-   If needed, grant rights to execute downloaded/compiled binaries
    using chmod (`chmod a+x BINARY_NAME`)
-   Move all executables to \$PATH folders (e.g.`/usr/local/bin`) to
    make them accessible without specifying the full path.
-   Typical command to run a container interactively (`-it`) and delete
    on exit(`--rm`): `docker run --rm -it name:tag`
-   \[1\] Use [hadolint](https://hadolint.github.io/hadolint/) and
    remove as many reported warnings as possible.
-   \[0.5\] Add relevant
    [labels](https://docs.docker.com/engine/reference/builder/#label),
    e.g. maintainer, version, etc.
    ([hint](https://medium.com/@chamilad/lets-make-your-docker-image-better-than-90-of-existing-ones-8b1e5de950d))
:::

::: {.cell .code id="ELmlPfIGOVQ_"}
``` {.python}
FROM ubuntu:18.04
RUN useradd --create-home --shell /bin/bash app_user
WORKDIR /home/app_user
USER root
RUN 	apt update	&& \
	apt-get update 	&& \
	apt-get install -y wget && 	\
	apt-get install -y make &&	\
	apt install -y openjdk-11-jdk &&\
	apt-get install -y unzip &&	\
	apt-get install -y git 	&&	\
	apt-get install -y python3-pip

# install fastqc rdy
RUN  	echo 'FastQC installation process begin'
RUN  	echo 'FastQC need java to run. So make sure u have it'
RUN	  wget https://www.bioinformatics.babraham.ac.uk/projects/fastqc/fastqc_v0.11.9.zip
RUN  	unzip fastqc_v0.11.9.zip && rm fastqc_v0.11.9.zip 
RUN   chmod a+x FastQC/fastqc
RUN   echo 'alias fastqc="/FastQC/fastqc"' >> /.bashrc
RUN  	echo 'U can run it now with "fastqc" cmd in terminal'


#install samtools rdy
RUN 	git clone -b 1.16.1 https://github.com/samtools/samtools.git
RUN	  mv samtools/misc samtools_tools && rm -R samtools 
RUN	  echo 'alias samtools="/samtools_tools/samtools.pl"' >> /.bashrc
RUN	  echo "samtools installed"

#gradle done
RUN 	wget https://services.gradle.org/distributions/gradle-7.6-bin.zip
RUN	  mkdir /opt/gradle && unzip -d /opt/gradle gradle-7.6-bin.zip &&\
	    rm gradle-7.6-bin.zip
RUN	  export PATH=$PATH:/opt/gradle/gradle-7.6/bin

#picard rdy
RUN	  git clone -b 2.27.5 https://github.com/broadinstitute/picard.git
RUN	  cd picard/ && ./gradlew shadowJar
RUN	  echo 'alias picard="java -jar ./picard/bin/picard.jar"' >> /.bashrc


#salmon v.1.9.0	
RUN   wget https://github.com/COMBINE-lab/salmon/releases/download/v1.9.0/salmon-1.9.0_linux_x86_64.tar.gz 
RUN   tar -zxvf salmon-1.9.0_linux_x86_64.tar.gz && rm salmon-1.9.0_linux_x86_64.tar.gz 
RUN   chmod a+x salmon-1.9.0_linux_x86_64/bin/salmon && \
      mv salmon-1.9.0_linux_x86_64/bin/salmon /bin/salmon && \
      rm -r salmon-1.9.0_linux_x86_64 
    
#STAR v.2.7.10b
RUN   wget https://github.com/alexdobin/STAR/releases/download/2.7.10b/STAR_2.7.10b.zip
RUN   unzip STAR_2.7.10b.zip && rm STAR_2.7.10b.zip 
RUN   chmod a+x STAR_2.7.10b/Linux_x86_64_static/STAR
RUN   mv STAR_2.7.10b/Linux_x86_64_static/STAR /bin/STAR && \
      rm -r STAR_2.7.10b


RUN pip3 install --upgrade pip    
RUN pip3 install multiqc==1.13
```
:::

::: {.cell .markdown id="k7BfQC_m1CFU"}
## Extra points \[1.5\] {#extra-points-15}

You will be awarded extra points for the following:

-   \[0.5\] Using [multi-stage
    builds](https://docs.docker.com/build/building/multi-stage/) in
    Docker. E.g. to build STAR and copy only the executable to the final
    image.

-   \[0.75\] Minimizing the size of the final Docker image. That is,
    removing all intermediates, unnecessary binaries/caches, etc. Don\'t
    forget to compare & report the final size before and after all the
    optimizations.

-   \[0.25\] Create an extra Dockerfile that starts from [a conda base
    image](https://hub.docker.com/r/continuumio/anaconda3) and builds
    everything from your conda environment file.

Hint: `conda env create --quiet -f environment.yml && conda clean -a`
([example](https://github.com/nf-core/clipseq/blob/master/Dockerfile))
:::
