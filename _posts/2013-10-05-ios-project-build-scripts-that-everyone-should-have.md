---
layout: post
title: iOS Project Build Scripts That Everyone Should Have
date: 2013-10-05 4:11:08
categories: ios apple xcode shell
---

Here are a couple build scripts that make my life easier:

XCode Build Version Bump
---------------------------------
Increments the build number after every build.

NOTE: This does not really make sense to do on multi developer projects.

{% highlight bash %}
buildNumber=$(/usr/libexec/PlistBuddy -c "Print CFBundleVersion" "${PROJECT_DIR}/${INFOPLIST_FILE}")
buildNumber=$(($buildNumber + 1))
/usr/libexec/PlistBuddy -c "Set :CFBundleVersion $buildNumber" "${PROJECT_DIR}/${INFOPLIST_FILE}"
{% endhighlight %}

XCode Archive Version Bump
---------------------------------
Increments the Version number after every archive that is generated.

{% highlight bash %}
VERSIONNUM=$(/usr/libexec/PlistBuddy -c "Print CFBundleShortVersionString" "${PROJECT_DIR}/${INFOPLIST_FILE}")
NEWSUBVERSION=`echo $VERSIONNUM | awk -F "." '{print $3}'`
NEWSUBVERSION=$(($NEWSUBVERSION + 1))
NEWVERSIONSTRING=`echo $VERSIONNUM | awk -F "." '{print $1 "." $2 ".'$NEWSUBVERSION'" }'`
/usr/libexec/PlistBuddy -c "Set :CFBundleShortVersionString $NEWVERSIONSTRING" "${PROJECT_DIR}/${INFOPLIST_FILE}"
{% endhighlight %}

Thank you to [sekati](https://gist.github.com/sekati) for his [gist](https://gist.github.com/sekati/3172554).
