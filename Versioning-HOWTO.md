Creating Great Version Strings
==============================

When you build and deploy a service, it's important to make it easy to
understand when it was built, and what code it contains. I prefer my 
version strings to look like this:

    1.0.275.b244a2b9b8-20151027.181836

Which is:

    <major>.<minor>.<commit#>-<Git SHA>-<date>.<time>

I build this from my Makefile or build script:

    MAJOR_VER="1"
    MINOR_VER="0"
    COMMIT_NUMBER=`git rev-list HEAD --count`
    COMMIT_SHA=`git rev-parse --verify HEAD | cut -c 1-10`
    BUILD_DATE=`date +%Y-%m-%d.%H%M%S`
    VERSION="${MAJOR_VER}.${MINOR_VER}.${COMMIT_NUMBER}-${COMMIT_SHA}-${BUILD_DATE}"


### Version Components


__major__: 

The major version - up to you to set; only increased when there are significant changes/improvements

__minor__

The minor version - up to you to set; ideally updated every release, but if you're like me, you'll forget

__commit#__

The number of Git commits up to this point - generally interesting, if not useful

__Git-SHA__

The SHA of the most recent Git commit. This is by far the most important component. Not sure if you deployed a fix for that huge bug? No problem, just find this commit ID in your Git log, and read through the history. That's not good enough, or you want to build this instance again? Check out the repository at this commit, and have fun!

__date__

The date of the build, with the format YYYY-MM-DD

__time__

The time of the build, with the format HHMMSS

