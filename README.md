# forensic-toolkit

Skip to:
* [Windows](https://github.com/clingeric/forensic-toolkit/#Windows)
* [Linux](https://github.com/clingeric/forensic-toolkit/#Linux)
* [Mac](https://github.com/clingeric/forensic-toolkit/#Mac)

## Windows

### Memory

#### [Rekall](http://www.rekall-forensic.com/)

##### Description
>Rekall is an advanced forensic and incident response framework. While it began life purely as a memory forensic framework, it has now evolved into a complete platform.  Rekall implements the most advanced analysis techniques in the field, while still being developed in the open, with a free and open source license. Many of the innovations implemented within Rekall have been published in peer reviewed papers .  

>Rekall provides an end-to-end solution to incident responders and forensic analysts. From state of the art acquisition tools, to the most advanced open source memory analysis framework. Rekall at a glance.

##### Review

Rekall is my favorite memory analysis tool. It's a powerful command-line tool that is able to run on any machine that runs Python. It's much easier to use than Volatility, because of both its ability to be run easily on Python, and its lack of needing a specific profile. 

In addition to being a memory analysis tool, Rekall comes with the PMem suite that allows for the acqusition of volatile memory. The PMem suite saves the volatile memory which allows one to analyze the memory with Rekall later. Specifically, on Windows, the tool is called WinPMem. 

##### Usage Notes

Must have Python installed on the machine for it to work. 

Install using: 

```shell
$ virtualenv  /tmp/MyEnv
New python executable in /tmp/MyEnv/bin/python
Installing setuptools, pip...done.
$ source /tmp/MyEnv/bin/activate
$ pip install --upgrade setuptools pip wheel
$ pip install rekall-agent rekall
```

#### [Volatility](https://github.com/volatilityfoundation/volatility)

##### Description
>The Volatility Framework is a completely open collection of tools, implemented in Python under the GNU General Public License, for the extraction of digital artifacts from volatile memory (RAM) samples. The extraction techniques are performed completely independent of the system being investigated but offer visibilty into the runtime state of the system. The framework is intended to introduce people to the techniques and complexities associated with extracting digital artifacts from volatile memory samples and provide a platform for further work into this exciting area of research.

##### Review
While Volatility provides many of the same features Rekall does (both Python based, both command-line based, both intended for memory analysis) Volatility requires the use of profiles, which are difficult to both obtain and use, especially if the computer you are working with is not a common OS release or is too new for a proper profile to have been built. Additionally, Volatility seems to be much slower than Rekall in performing standard memory analysis procedures. 

##### Usage Notes
Installation:

>Extract the archive and run setup.py. This will take care of copying files to the right locations on your disk. Running setup.py is only necessary if you want to have access to the Volatility namespace from other Python scripts, for example if you plan on importing Volatility as a library. Pros: easy use as a library. Cons: more difficult to upgrade or uninstall.

>Extract the archive to a directory of your choice. When you want to use Volatility just do python /path/to/directory/vol.py. This is a cleaner method since no files are ever moved outside of your chosen directory, which makes it easier to upgrade to new versions when they're released. Also, you can easily have multiple versions of Volatility installed at the same time, by just keeping them in separate directories (like /home/me/vol2.0 and /home/me/vol2.1). Pros: clean, easy to run multiple versions, easy to upgrade or uninstall. Cons: more difficult to use as a library.

Additionally, you must obtain the profile information first before running any other tool. You can do this with:

```shell
volatility -f <memory capture> imageinfo
```

### Host

#### [FTK](https://accessdata.com/product-download?/support/product-downloads)

##### Description
>Forensic Toolkit, or FTK, is a computer forensics software made by AccessData. It scans a hard drive looking for various information. It can, for example, locate deleted emails and scan a disk for text strings to use them as a password dictionary to crack encryption. 

##### Review
While FTK is a very powerful tool, it offers essentially the same functionality of Autopsy and Redline, but in a much less user-friendly package. As a novice forensic investigator, I would probably never know the large differences between FTK and Autopsy, but since Autopsy is easier for me to use, I would never pick FTK unless nothing else worked.

##### Usage Notes
FTK can be installed using a `.exe` file. The license may only be good until I graduate.

#### [FTK Imager](https://accessdata.com/product-download?/support/product-downloads)

##### Description
>The FTK Imager is a simple but concise tool. It saves an image of a hard disk in one file or in segments that may be later on reconstructed. It calculates MD5 hash values and confirms the integrity of the data before closing the files. 

##### Review
FTK Imager is a really simple and slick program. It can be used for both live and dead acquistions which makes it incredibly valuable for obtaining images from a computer. It outputs multiple formats to then be analyzed using an image analysis program like Autopsy. 

##### Usage Notes
Be sure to bring and use a write blocker to assure that you aren't writing any data to the disk you're trying to image. Failing to do so can invalidate the evidence on that disk.

#### [WinPrefetchView](https://www.nirsoft.net/utils/win_prefetch_view.html)

##### Description
>WinPrefetchView is a small utility that reads the Prefetch files stored in your system and displays the information stored in them. By looking in these files, you can learn which files every application is using, and which files are loaded on Windows boot. 

##### Review
WinPrefetchView is a great, simple tool that really helps determine the root cause of suspicious activity. It helps piece together eveidence and recorded stories to identify IOCs and initial compromises of the system. Although Prefetch files can be deleted or tampered with, it's not always the most fool-proof method, it's a great starting place to start an analysis of a victim's machine.

##### Usage Notes
To use WinPrefetchView on Prefetch files obtained from a victim's machine, you need to change the source of the files by navigating to the Options Menu, selecting Advanced Options, and then change the directory of the Prefectch files.

#### [Redline](https://www.fireeye.com/services/freeware/redline.html)

##### Description
>Redline®, FireEye's premier free endpoint security tool, provides host investigative capabilities to users to find signs of malicious activity through memory and file analysis and the development of a threat assessment profile. 

Redline has very similar functionality to Autopsy and FTK.

##### Review

I personally have never used Redline, but according to the other people who I know, it's almost as good as Autopsy in performing host analysis. Additionally, since it's part of the FireEye software suite, there's a lot of interoperability. Additionally, Redline can assist with finding IOCs. I would use it only if Autopsy cannot be used, but I would prefer it over FTK.

##### Usage Notes
Redline is installed with an `.exe` file, and cannot be used with Linux or MacOSX. 

#### [Autopsy](https://www.sleuthkit.org/autopsy/)

##### Description
>Autopsy® is a digital forensics platform and graphical interface to The Sleuth Kit® and other digital forensics tools. It is used by law enforcement, military, and corporate examiners to investigate what happened on a computer. You can even use it to recover photos from your camera's memory card.

Autopsy does host analysis, similar to FTK and Redline.

##### Review
I really like Autopsy. It's powerful yet simple to use. It's my preferred host analysis software. One of the best features of Autopsy is the ability to import modules that can add enhanced functionality to the software. For example, by adding the "Interesting Files" module, it will perform a scan for you looking for files that could be potential IOCs, like inserted USB drives. The GUI is streamlined and simple to use. The search feature is very powerful and can find files on the image very quickly. 

##### Usage Notes
Although the import modules provide a lot of functionality, not selecting them in the original import drastically speeds the loading and indexing process. The Timeline Analysis is also really interesting when you don't have the full story of what occured. 

### Network

#### [Wireshark](https://www.wireshark.org/download.html)

##### Description
>Wireshark is the world’s foremost network protocol analyzer. It lets you see what’s happening on your network at a microscopic level. It is the de facto (and often de jure) standard across many industries and educational institutions. Wireshark development thrives thanks to the contributions of networking experts across the globe.

Wireshark allows for active packet capture when your machine is connected to the network of interest. Additionally, Wireshark allows for offline packet analysis of saved network capture files (usually pcap). Wireshark allows for simple searching and filtering of packet types and contents to allow investigators to identify potentially dangerous network traffic. 

##### Review
Wireshark is both powerful and simple. The best feature is the ability to filter and search through the traffic. The downside to Wireshark is that it requires that the analyst have a good idea of what happened and approximately when it happened. Unlike Autopsy, it doesn't highlight interesting files or packets, and requires the analyst to perform all of the work manually. Despite this annoyance, it's by far the most powerful network analysis tool. 

##### Usage Notes
Wireshark doesn't respond well to large network capture files. It's available in an `.exe` installer on Windows.

#### [Nmap](https://nmap.org/download.html)

##### Description
>Nmap (Network Mapper) is a free and open-source network scanner. Nmap is used to discover hosts and services on a computer network by sending packets and analyzing the responses.Nmap provides a number of features for probing computer networks, including host discovery and service and operating system detection. These features are extensible by scripts that provide more advanced service detection, vulnerability detection, and other features. Nmap can adapt to network conditions including latency and congestion during a scan. 

Nmap is useful for getting a overview of the network conditions of a machine durinthe acqusition phase. It can also obtain additional network information that can be analyzed at later steps. 

##### Review
Nmap is very streamlined and simple. It's a command-line tool that offers a robust set of features. It's my go-to software for obtaining information about a machine's network connections, layout, and other relevant info. 

##### Usage Notes
Nnap is usually installed on most machines, but can be installed with a `.exe` file on Windows.

#### [Snort](https://www.snort.org/downloads)

##### Description
>Snort is a free open source network intrusion detection system (IDS) and intrusion prevention system (IPS). Snort's can perform real-time traffic analysis and packet logging on Internet Protocol (IP) networks. Snort performs protocol analysis, content searching and matching. The program can also be used to detect probes or attacks, including, but not limited to, operating system fingerprinting attempts, semantic URL attacks, buffer overflows, server message block probes, and stealth port scans. Additionally, Snort will monitor network traffic and analyze it against a rule set defined by the user. The program will then perform a specific action based on what has been identified.

##### Review
Snort is a great tool for network analysis. However, its effectiveness is only as good as its rules list. If the rules list is not up to date, Snort will not be able to identify any suspicious network traffic. Otherwise, it's a relatively straightforward program. Another disadvantage of Snort is the installation process, which can be tedious and error-prone. Once installed, however, it's simple to use. 

##### Usage Notes
Snort can be used for live monitoring or offline, dead analysis. Be sure to get the newest ruleset. 

### Malware

#### [VirusTotal](https://www.virustotal.com/)

##### Description
>VirusTotal aggregates many antivirus products and online scan engines to check for viruses that the user's own antivirus may have missed, or to verify against any false positives. Users can scan suspect URLs, upload files, or upload file hashes to search through the VirusTotal dataset.

##### Review
VirusTotal is an incredible website that provides fast and simple virus detection. My favorite feature is the ability to search for malware by hash, eliminating the need to upload the potentially dangerous file through your web browswer. VirusTotal also has exposed APIs that allow for the malware indentification to take place in an automated fashion. Its malware lists are continually being update to assure that malware will be properly detected. 

##### Usage Notes
VirusTotal is available only online. In addition to the static analysis VirusTotal perform, you can perform dynamic analysis using its uploaded Cuckoo sandbox.

#### [Ghidra](https://ghidra-sre.org/)

##### Description
>Ghidra is a software reverse engineering (SRE) framework created and maintained by the National Security Agency Research Directorate. This framework includes a suite of full-featured, high-end software analysis tools that enable users to analyze compiled code on a variety of platforms including Windows, macOS, and Linux. Capabilities include disassembly, assembly, decompilation, graphing, and scripting, along with hundreds of other features. Ghidra supports a wide variety of processor instruction sets and executable formats and can be run in both user-interactive and automated modes. Users may also develop their own Ghidra plug-in components and/or scripts using Java or Python.

##### Review
I've personally never used Ghidra, but I've heard from many professionals that it provides an incredible amout of features for a free software. Although I don't know much about reverse engineering of malware, I would use Ghidra to assist me. 

##### Usage Notes
Requires Python to be installed. 

## Linux

### Memory

#### [Rekall](http://www.rekall-forensic.com/)

##### Description
>Rekall is an advanced forensic and incident response framework. While it began life purely as a memory forensic framework, it has now evolved into a complete platform.  Rekall implements the most advanced analysis techniques in the field, while still being developed in the open, with a free and open source license. Many of the innovations implemented within Rekall have been published in peer reviewed papers .  

>Rekall provides an end-to-end solution to incident responders and forensic analysts. From state of the art acquisition tools, to the most advanced open source memory analysis framework. Rekall at a glance.

##### Review

Rekall is my favorite memory analysis tool. It's a powerful command-line tool that is able to run on any machine that runs Python. It's much easier to use than Volatility, because of both its ability to be run easily on Python, and its lack of needing a specific profile. 

In addition to being a memory analysis tool, Rekall comes with the PMem suite that allows for the acqusition of volatile memory. The PMem suite saves the volatile memory which allows one to analyze the memory with Rekall later. Specifically, on Linux, the tool is called LinPMem. 

##### Usage Notes

Must have Python installed on the machine for it to work. 

Install using: 

```shell
$ virtualenv  /tmp/MyEnv
New python executable in /tmp/MyEnv/bin/python
Installing setuptools, pip...done.
$ source /tmp/MyEnv/bin/activate
$ pip install --upgrade setuptools pip wheel
$ pip install rekall-agent rekall
```


#### [Volatility](https://github.com/volatilityfoundation/volatility)

##### Description
>The Volatility Framework is a completely open collection of tools, implemented in Python under the GNU General Public License, for the extraction of digital artifacts from volatile memory (RAM) samples. The extraction techniques are performed completely independent of the system being investigated but offer visibilty into the runtime state of the system. The framework is intended to introduce people to the techniques and complexities associated with extracting digital artifacts from volatile memory samples and provide a platform for further work into this exciting area of research.

##### Review
While Volatility provides many of the same features Rekall does (both Python based, both command-line based, both intended for memory analysis) Volatility requires the use of profiles, which are difficult to both obtain and use, especially if the computer you are working with is not a common OS release or is too new for a proper profile to have been built. Additionally, Volatility seems to be much slower than Rekall in performing standard memory analysis procedures. 

##### Usage Notes
Installation:

>Extract the archive and run setup.py. This will take care of copying files to the right locations on your disk. Running setup.py is only necessary if you want to have access to the Volatility namespace from other Python scripts, for example if you plan on importing Volatility as a library. Pros: easy use as a library. Cons: more difficult to upgrade or uninstall.

>Extract the archive to a directory of your choice. When you want to use Volatility just do python /path/to/directory/vol.py. This is a cleaner method since no files are ever moved outside of your chosen directory, which makes it easier to upgrade to new versions when they're released. Also, you can easily have multiple versions of Volatility installed at the same time, by just keeping them in separate directories (like /home/me/vol2.0 and /home/me/vol2.1). Pros: clean, easy to run multiple versions, easy to upgrade or uninstall. Cons: more difficult to use as a library.

Additionally, you must obtain the profile information first before running any other tool. You can do this with:

```shell
volatility -f <memory capture> imageinfo
```

#### [LiME](https://github.com/504ensicsLabs/LiME)

##### Description
>A Loadable Kernel Module (LKM) which allows for volatile memory acquisition from Linux and Linux-based devices, such as Android. This makes LiME unique as it is the first tool that allows for full memory captures on Android devices. It also minimizes its interaction between user and kernel space processes during acquisition, which allows it to produce memory captures that are more forensically sound than those of other tools designed for Linux memory acquisition.

##### Review
Lime is simple and relatively easy to use, once it's been built from source and installed. Given its similar functionality to Rekall's PMem suite and LinPMem, I would prefer to use LinPMem over LiME due to the need to not build from source and the similar functionality across the PMem suite.

##### Usage Notes
Lime must be built from source (depending on your distribution), so be sure to build it on your device and not on the device of the machine you are going to be capturing data from, as to assure evidence integrity.

```shell
insmod ./lime.ko "path=<outfile | tcp:<port>> format=<raw|padded|lime> [digest=<digest>] [dio=<0|1>]"

path (required):   outfile ~ name of file to write to on local system (SD Card)
                   tcp:port ~ network port to communicate over
        
format (required): padded ~ pads all non-System RAM ranges with 0s
                   lime ~ each range prepended with fixed-size header containing address space info
                   raw ~ concatenates all System RAM ranges (warning : original position of dumped memory is likely to be lost)

digest (optional): Hash the RAM and provide a .digest file with the sum.
                   Supports kernel version 2.6.11 and up. See below for
                   available digest options.

dio (optional):    1 ~ attempt to enable Direct IO
                   0 ~ default, do not attempt Direct IO
        
localhostonly (optional):  1 ~ restricts the tcp to only listen on localhost,
                           0 ~ binds on all interfaces (default)

timeout (optional): 1000 ~ max amount of milliseconds tolerated to read a page (default).
                           If a page exceeds the timeout all the memory region are skipped.
                       0 ~ disable the timeout so the slow region will be acquired.

                           This feature is only available on kernel versions >= 2.6.35. 
```

### Host

#### [Autopsy](https://www.sleuthkit.org/autopsy/)

##### Description
>Autopsy® is a digital forensics platform and graphical interface to The Sleuth Kit® and other digital forensics tools. It is used by law enforcement, military, and corporate examiners to investigate what happened on a computer. You can even use it to recover photos from your camera's memory card.

Autopsy does host analysis, similar to FTK and Redline.

##### Review
I really like Autopsy. It's powerful yet simple to use. It's my preferred host analysis software. One of the best features of Autopsy is the ability to import modules that can add enhanced functionality to the software. For example, by adding the "Interesting Files" module, it will perform a scan for you looking for files that could be potential IOCs, like inserted USB drives. The GUI is streamlined and simple to use. The search feature is very powerful and can find files on the image very quickly. 

##### Usage Notes
Although the import modules provide a lot of functionality, not selecting them in the original import drastically speeds the loading and indexing process. The Timeline Analysis is also really interesting when you don't have the full story of what occured. 

### Network

#### [Netcat](http://netcat.sourceforge.net/)

##### Description
>netcat (often abbreviated to nc) is a computer networking utility for reading from and writing to network connections using TCP or UDP. The command is designed to be a dependable back-end that can be used directly or easily driven by other programs and scripts. At the same time, it is a feature-rich network debugging and investigation tool, since it can produce almost any kind of connection its user could need and has a number of built-in capabilities. 

##### Review
Netcat is a very streamlined and powerful command-line network utility. It's available by default on almost OS, which makes it powerful as understanding is OS agnostic. It's able to provide quick status readouts of the network and connected devices. It's very similar to nmap, but lacks some of its features. Howerver, nmap is the default way to install netcat on Windows, so the two tools go hand in hand for network analysis. 

##### Usage Notes
If not installed on machine, it must be installed as a `.rpm` file or built from source for other distributions.

### Network

#### [Wireshark](https://www.wireshark.org/download.html)

##### Description
>Wireshark is the world’s foremost network protocol analyzer. It lets you see what’s happening on your network at a microscopic level. It is the de facto (and often de jure) standard across many industries and educational institutions. Wireshark development thrives thanks to the contributions of networking experts across the globe.

Wireshark allows for active packet capture when your machine is connected to the network of interest. Additionally, Wireshark allows for offline packet analysis of saved network capture files (usually pcap). Wireshark allows for simple searching and filtering of packet types and contents to allow investigators to identify potentially dangerous network traffic. 

##### Review
Wireshark is both powerful and simple. The best feature is the ability to filter and search through the traffic. The downside to Wireshark is that it requires that the analyst have a good idea of what happened and approximately when it happened. Unlike Autopsy, it doesn't highlight interesting files or packets, and requires the analyst to perform all of the work manually. Despite this annoyance, it's by far the most powerful network analysis tool. 

##### Usage Notes
Wireshark doesn't respond well to large network capture files. It's available as a package for most distributions and is available in `apt`.

##### Description
>Nmap (Network Mapper) is a free and open-source network scanner. Nmap is used to discover hosts and services on a computer network by sending packets and analyzing the responses.Nmap provides a number of features for probing computer networks, including host discovery and service and operating system detection. These features are extensible by scripts that provide more advanced service detection, vulnerability detection, and other features. Nmap can adapt to network conditions including latency and congestion during a scan. 

Nmap is useful for getting a overview of the network conditions of a machine durinthe acqusition phase. It can also obtain additional network information that can be analyzed at later steps. 

##### Review
Nmap is very streamlined and simple. It's a command-line tool that offers a robust set of features. It's my go-to software for obtaining information about a machine's network connections, layout, and other relevant info. 

##### Usage Notes
Nnap is usually installed on most machines, but can be installed with a `apt` or other package installers in addition to the packages available from the website.

#### [Snort](https://www.snort.org/downloads)

##### Description
>Snort is a free open source network intrusion detection system (IDS) and intrusion prevention system (IPS). Snort's can perform real-time traffic analysis and packet logging on Internet Protocol (IP) networks. Snort performs protocol analysis, content searching and matching. The program can also be used to detect probes or attacks, including, but not limited to, operating system fingerprinting attempts, semantic URL attacks, buffer overflows, server message block probes, and stealth port scans. Additionally, Snort will monitor network traffic and analyze it against a rule set defined by the user. The program will then perform a specific action based on what has been identified.

##### Review
Snort is a great tool for network analysis. However, its effectiveness is only as good as its rules list. If the rules list is not up to date, Snort will not be able to identify any suspicious network traffic. Otherwise, it's a relatively straightforward program. Another disadvantage of Snort is the installation process, which can be tedious and error-prone. Once installed, however, it's simple to use. 

##### Usage Notes
Snort can be used for live monitoring or offline, dead analysis. Be sure to get the newest ruleset. 

### Malware

#### [VirusTotal](https://www.virustotal.com/)

##### Description
>VirusTotal aggregates many antivirus products and online scan engines to check for viruses that the user's own antivirus may have missed, or to verify against any false positives. Users can scan suspect URLs, upload files, or upload file hashes to search through the VirusTotal dataset.

##### Review
VirusTotal is an incredible website that provides fast and simple virus detection. My favorite feature is the ability to search for malware by hash, eliminating the need to upload the potentially dangerous file through your web browswer. VirusTotal also has exposed APIs that allow for the malware indentification to take place in an automated fashion. Its malware lists are continually being update to assure that malware will be properly detected. 

##### Usage Notes
VirusTotal is available only online. In addition to the static analysis VirusTotal perform, you can perform dynamic analysis using its uploaded Cuckoo sandbox.

#### [Ghidra](https://ghidra-sre.org/)

##### Description
>Ghidra is a software reverse engineering (SRE) framework created and maintained by the National Security Agency Research Directorate. This framework includes a suite of full-featured, high-end software analysis tools that enable users to analyze compiled code on a variety of platforms including Windows, macOS, and Linux. Capabilities include disassembly, assembly, decompilation, graphing, and scripting, along with hundreds of other features. Ghidra supports a wide variety of processor instruction sets and executable formats and can be run in both user-interactive and automated modes. Users may also develop their own Ghidra plug-in components and/or scripts using Java or Python.

##### Review
I've personally never used Ghidra, but I've heard from many professionals that it provides an incredible amout of features for a free software. Although I don't know much about reverse engineering of malware, I would use Ghidra to assist me. 

##### Usage Notes
Requires Python to be installed. 

## Mac

### Memory

#### [Rekall](http://www.rekall-forensic.com/)

##### Description
>Rekall is an advanced forensic and incident response framework. While it began life purely as a memory forensic framework, it has now evolved into a complete platform.  Rekall implements the most advanced analysis techniques in the field, while still being developed in the open, with a free and open source license. Many of the innovations implemented within Rekall have been published in peer reviewed papers .  

>Rekall provides an end-to-end solution to incident responders and forensic analysts. From state of the art acquisition tools, to the most advanced open source memory analysis framework. Rekall at a glance.

##### Review

Rekall is my favorite memory analysis tool. It's a powerful command-line tool that is able to run on any machine that runs Python. It's much easier to use than Volatility, because of both its ability to be run easily on Python, and its lack of needing a specific profile. 

In addition to being a memory analysis tool, Rekall comes with the PMem suite that allows for the acqusition of volatile memory. The PMem suite saves the volatile memory which allows one to analyze the memory with Rekall later. Specifically, on Mac, the tool is called OSXPMem. 

##### Usage Notes

Must have Python installed on the machine for it to work. 

Install using: 

```shell
$ virtualenv  /tmp/MyEnv
New python executable in /tmp/MyEnv/bin/python
Installing setuptools, pip...done.
$ source /tmp/MyEnv/bin/activate
$ pip install --upgrade setuptools pip wheel
$ pip install rekall-agent rekall
```

#### [Volatility](https://github.com/volatilityfoundation/volatility)

##### Description
>The Volatility Framework is a completely open collection of tools, implemented in Python under the GNU General Public License, for the extraction of digital artifacts from volatile memory (RAM) samples. The extraction techniques are performed completely independent of the system being investigated but offer visibilty into the runtime state of the system. The framework is intended to introduce people to the techniques and complexities associated with extracting digital artifacts from volatile memory samples and provide a platform for further work into this exciting area of research.

##### Review
While Volatility provides many of the same features Rekall does (both Python based, both command-line based, both intended for memory analysis) Volatility requires the use of profiles, which are difficult to both obtain and use, especially if the computer you are working with is not a common OS release or is too new for a proper profile to have been built. Additionally, Volatility seems to be much slower than Rekall in performing standard memory analysis procedures. 

##### Usage Notes
Installation:

>Extract the archive and run setup.py. This will take care of copying files to the right locations on your disk. Running setup.py is only necessary if you want to have access to the Volatility namespace from other Python scripts, for example if you plan on importing Volatility as a library. Pros: easy use as a library. Cons: more difficult to upgrade or uninstall.

>Extract the archive to a directory of your choice. When you want to use Volatility just do python /path/to/directory/vol.py. This is a cleaner method since no files are ever moved outside of your chosen directory, which makes it easier to upgrade to new versions when they're released. Also, you can easily have multiple versions of Volatility installed at the same time, by just keeping them in separate directories (like /home/me/vol2.0 and /home/me/vol2.1). Pros: clean, easy to run multiple versions, easy to upgrade or uninstall. Cons: more difficult to use as a library.

Additionally, you must obtain the profile information first before running any other tool. You can do this with:

```shell
volatility -f <memory capture> imageinfo
```

### Host

#### [Autopsy](https://www.sleuthkit.org/autopsy/)

##### Description
>Autopsy® is a digital forensics platform and graphical interface to The Sleuth Kit® and other digital forensics tools. It is used by law enforcement, military, and corporate examiners to investigate what happened on a computer. You can even use it to recover photos from your camera's memory card.

Autopsy does host analysis, similar to FTK and Redline.

##### Review
I really like Autopsy. It's powerful yet simple to use. It's my preferred host analysis software. One of the best features of Autopsy is the ability to import modules that can add enhanced functionality to the software. For example, by adding the "Interesting Files" module, it will perform a scan for you looking for files that could be potential IOCs, like inserted USB drives. The GUI is streamlined and simple to use. The search feature is very powerful and can find files on the image very quickly. 

##### Usage Notes
Although the import modules provide a lot of functionality, not selecting them in the original import drastically speeds the loading and indexing process. The Timeline Analysis is also really interesting when you don't have the full story of what occured. 


### Network

#### [Netcat](http://netcat.sourceforge.net/)

##### Description
##### Review
##### Usage Notes

#### [Wireshark](https://www.wireshark.org/download.html)

##### Description
>Wireshark is the world’s foremost network protocol analyzer. It lets you see what’s happening on your network at a microscopic level. It is the de facto (and often de jure) standard across many industries and educational institutions. Wireshark development thrives thanks to the contributions of networking experts across the globe.

Wireshark allows for active packet capture when your machine is connected to the network of interest. Additionally, Wireshark allows for offline packet analysis of saved network capture files (usually pcap). Wireshark allows for simple searching and filtering of packet types and contents to allow investigators to identify potentially dangerous network traffic. 

##### Review
Wireshark is both powerful and simple. The best feature is the ability to filter and search through the traffic. The downside to Wireshark is that it requires that the analyst have a good idea of what happened and approximately when it happened. Unlike Autopsy, it doesn't highlight interesting files or packets, and requires the analyst to perform all of the work manually. Despite this annoyance, it's by far the most powerful network analysis tool. 

##### Usage Notes
Wireshark doesn't respond well to large network capture files. It's available in a package for Mac or through `brew`.

#### [Nmap](https://nmap.org/download.html)

##### Description
>Nmap (Network Mapper) is a free and open-source network scanner. Nmap is used to discover hosts and services on a computer network by sending packets and analyzing the responses.Nmap provides a number of features for probing computer networks, including host discovery and service and operating system detection. These features are extensible by scripts that provide more advanced service detection, vulnerability detection, and other features. Nmap can adapt to network conditions including latency and congestion during a scan. 

Nmap is useful for getting a overview of the network conditions of a machine durinthe acqusition phase. It can also obtain additional network information that can be analyzed at later steps. 

##### Review
Nmap is very streamlined and simple. It's a command-line tool that offers a robust set of features. It's my go-to software for obtaining information about a machine's network connections, layout, and other relevant info. 

##### Usage Notes
Nnap is usually installed on most machines, but can be installed with a package from the website or through `brew`
#### Snort

##### Description
>Snort is a free open source network intrusion detection system (IDS) and intrusion prevention system (IPS). Snort's can perform real-time traffic analysis and packet logging on Internet Protocol (IP) networks. Snort performs protocol analysis, content searching and matching. The program can also be used to detect probes or attacks, including, but not limited to, operating system fingerprinting attempts, semantic URL attacks, buffer overflows, server message block probes, and stealth port scans. Additionally, Snort will monitor network traffic and analyze it against a rule set defined by the user. The program will then perform a specific action based on what has been identified.

##### Review
Snort is a great tool for network analysis. However, its effectiveness is only as good as its rules list. If the rules list is not up to date, Snort will not be able to identify any suspicious network traffic. Otherwise, it's a relatively straightforward program. Another disadvantage of Snort is the installation process, which can be tedious and error-prone. Once installed, however, it's simple to use. 

##### Usage Notes
Snort can be used for live monitoring or offline, dead analysis. Be sure to get the newest ruleset. 

Snort isn't available for Mac through it's website, but is available through `brew`

```shell
brew install snort
```

### Malware

#### [VirusTotal](https://www.virustotal.com/)

##### Description
>VirusTotal aggregates many antivirus products and online scan engines to check for viruses that the user's own antivirus may have missed, or to verify against any false positives. Users can scan suspect URLs, upload files, or upload file hashes to search through the VirusTotal dataset.

##### Review
VirusTotal is an incredible website that provides fast and simple virus detection. My favorite feature is the ability to search for malware by hash, eliminating the need to upload the potentially dangerous file through your web browswer. VirusTotal also has exposed APIs that allow for the malware indentification to take place in an automated fashion. Its malware lists are continually being update to assure that malware will be properly detected. 

##### Usage Notes
VirusTotal is available only online. In addition to the static analysis VirusTotal perform, you can perform dynamic analysis using its uploaded Cuckoo sandbox.

#### [Ghidra](https://ghidra-sre.org/)

##### Description
>Ghidra is a software reverse engineering (SRE) framework created and maintained by the National Security Agency Research Directorate. This framework includes a suite of full-featured, high-end software analysis tools that enable users to analyze compiled code on a variety of platforms including Windows, macOS, and Linux. Capabilities include disassembly, assembly, decompilation, graphing, and scripting, along with hundreds of other features. Ghidra supports a wide variety of processor instruction sets and executable formats and can be run in both user-interactive and automated modes. Users may also develop their own Ghidra plug-in components and/or scripts using Java or Python.

##### Review
I've personally never used Ghidra, but I've heard from many professionals that it provides an incredible amout of features for a free software. Although I don't know much about reverse engineering of malware, I would use Ghidra to assist me. 

##### Usage Notes
Requires Python to be installed. 
