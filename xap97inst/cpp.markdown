---
layout: post
title:  C++
categories: XAP97INST
parent: none
weight: 500
---


{% summary %}Requirements and how to install GigaSpaces c++ on Windows and Linux.{% endsummary %}

# Overview

GigaSpaces c++ API supported on Linux and Windows 32bit or 64bit machines.


{%note title=System Requirements%}For a list of supported platforms please consult [the realease notes](/release_notes) {%endnote%}


#  Installation

GigaSpaces XAP.NET is packaged as a standard Windows Installer package (.msi file). To start the installation simply double-click the msi file, and the installation wizard will pop up and guide you through the installation process.

Once you accept the licence agreement, you will be asked to choose a setup type. Select 'Complete' to install all the features in the default path (C:\GigaSpaces\XAP.NET 9.5.0). Selecting 'Custom' will allow you to customize the installation path, which features will be installed, and more.

## Other Installation Options

GigaSpaces XAP.NET offers more installation scenarios and customizations. For example:

- Command-line installation.
- Packaging XAP.NET in another installation package.
- Side-by-side installations.
- Using a different jvm.



{% exclamation %} Prior to installation, see the **[GigaSpaces installation prerequisites](./installation.html#Prior-to-Installation)**.

# Installation

1. Download the c++ API file that suits your platform.
1. Unzip the file into your `<GigaSpaces Root>` directory (download GigaSpaces [here](http://www.gigaspaces.com/LatestProductVersion)), using your favorite unzip tool (.e.g WinZip). For example - On linux you should run the following to install the C++ libraries:

{% highlight java %}
tar -xzvf gigaspaces-cpp-{{ site.latest_xap_version }}-ga-linux-amd64-gcc-4.1.2.tar.gz
{% endhighlight %}

Where the `gigaspaces-cpp-9.X.X-ga-linux-amd64-gcc-4.1.2.tar.gz` should be located at the `/gigaspaces-xap-premium-9.X.X-ga` folder.

1. After unzipping the ZIP file, you should have the following files and folders under your `<GigaSpaces Root>\cpp` folder:

{% indent %}
![CppTree.PNG](/attachment_files/CppTree.PNG)
{% endindent %}

{%anchor setting-the-environment %}

# Setting the Environment

There are several environment settings that are necessary to build and run the examples that come with this package. This section lists these settings. Choose the tab below that matches your platform.

{% inittab Environment_Settings %}
{% tabcontent Windows %}

## Environment Variables

The following environment variables need to be defined:

- **`JSHOMEDIR`** -- the `<GigaSpaces Root>` directory.
- **`PLATFORM`** -- the build platform, in this case win32 or win64.
- **`COMPILER`** -- the compiler used for building, for example: VS9.0.
- **`PATH`** -- This should include the compiler folder , GigaSpaces gsxml2cpp location and the jvm.dll location

For example:

    set JSHOMEDIR=C:\{{ site.latest_gshome_dirname }}
    set PLATFORM=win32
    set COMPILER=VS9.0

In addition, for windows 32 bit the **`PATH`** variable should be updated to include:

    %JSHOMEDIR%\cpp\lib\%PLATFORM%\%COMPILER%;%JSHOMEDIR%\cpp\bin\%PLATFORM%\%COMPILER%;%JAVA_HOME%\jre\bin\client

For windows 64 bit the **`PATH`** variable should be updated to include:

    %JSHOMEDIR%\cpp\lib\%PLATFORM%\%COMPILER%;%JSHOMEDIR%\cpp\bin\%PLATFORM%\%COMPILER%;%JAVA_HOME%\jre\bin\server

## Environment Script Files

If you don't want to set these variables globally (by defining System Variables) then the GigaSpaces C++ package includes the following script files that help set the environment:

- **`<GigaSpaces Root>\cpp\env.cmd`** -- Running this file defines these variables to match your platform.
- **`<GigaSpaces Root>\cpp\GigaVisualStudio.bat`** -- Running this file starts **Visual Studio** and automatically sets the environment.

{% exclamation %} You might need to edit these files to include the correct values for the `PATH` , `JAVA_HOME` and `JSHOMEDIR` environment variables and the correct location of Visual Studio and the jvm.dll.

{% endtabcontent %}
{% tabcontent Linux %}

## Environment Variables

The following environment variables need to be defined:

- **`JSHOMEDIR`** -- the `<GigaSpaces Root>` directory.
- **`PLATFORM`** -- the build platform, in this case linux-amd64 or linux32.
- **`COMPILER`** -- the compiler used for building, for example: gcc-4.1.2.

Example:

    JSHOMEDIR=../../..
    PLATFORM=linux-amd64
    COMPILER=gcc-4.1.2

## Environment Script Files

If you don't want to set these variables globally the GigaSpaces C++ package includes the following script file that help set the environment:

- **`<GigaSpaces Root>/cpp/setenv.sh`** -- Running this file defines these variables to match your platform.
{% endtabcontent %}
{% endinittab %}

# Testing the Installation

The package provides the following scripts (placed in `<GigaSpaces Root>\cpp`):

- **sanity** -- Run sanity tests on embedded, remote and partitioned space
- **runBenchmark** -- Run benchmark tests on embedded space
- **runTest** -- Run all functional tests on embedded space
- **testJiniTransactions** -- Run benchmark and functional tests on partitioned space using Jini Mahalo transactions

Result files can be found in `<GigaSpaces Root>\cpp`:

`benchmarkResult*.txt`  -- Benchmark tests results
`testResult*.xml` -- Functional tests results

{% panel title= | borderStyle=solid %}
{% lampon %} **What's next?**

- [Write your first C++ Application](./cpp-api-hello-world-example.html)
- Return to the [C++ homepage](./xap-cpp.html)
{% endpanel %}
