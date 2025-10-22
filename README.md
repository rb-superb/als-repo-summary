# als-repo-summary
Homework summary

Repo A: https://github.com/rb-superb/als-repo-a
Repo C: https://github.com/rb-superb/als-repo-c

Questions
o How did you test your pipelines?
>>ANS: By deploying jenkins in kubernetes cluster as a single Built-In Node as an executer. Kubernetes cluster is running under docker desktop on Windows machine. As my approach is to not depend on any plugins in Jenkins or installing any dependencies through pipeline due to security practices, I decided to modify and re-complile new jenkins docker image by using following dockerfile:

FROM jenkins/jenkins:lts
USER root

RUN apt-get update && \
    apt-get install -y \
    python3 \
    python3-pip \
    doxygen \
    && rm -rf /var/lib/apt/lists/*

RUN update-alternatives --install /usr/bin/python python /usr/bin/python3 1 && \
    update-alternatives --install /usr/bin/pip pip /usr/bin/pip3 1

USER jenkins

o How did you test repoC python?
>>ANS: By haveing tools ready on both executor Windows machine and jenkins modified docker image running in kubernetes cluster. I first tested it in my host Window machine to understand how doxygen produce to log out put and uses the python log parser with the doxygen log output as a parameter. Lastly, I then applied it to the jenkins declarive script pipeline and run it inside jenkins.

Executor tools:
Doxygen v1.14.0 (cbe58f6237b2238c9af7f51c6b7afb8bbf52c866)
Python 3.13.5

o What is the advantage to use LFS?
>>ANS: It help tracks large binary files using small text pointers to keep the repository history lean, making cloning and fetching much faster while still preserves normal git commands.

o How to adjust this repository to support LFS?
>>ANS: Once we need to installed and setup LFS, we need to migrate existing large files in the history to use Git LFS
>> $ git lfs migrate import --include="*.psd" --everything

and verify Git LFS tracking
>> $ git lfs ls-files

Reference link used: 
- https://docs.github.com/en/repositories/working-with-files/managing-large-files/installing-git-large-file-storage
- https://github.com/git-lfs/git-lfs#getting-started
