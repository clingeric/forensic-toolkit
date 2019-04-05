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

[Volatility](https://github.com/volatilityfoundation/volatility)

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

FTK

##### Description
>Forensic Toolkit, or FTK, is a computer forensics software made by AccessData. It scans a hard drive looking for various information. It can, for example, locate deleted emails and scan a disk for text strings to use them as a password dictionary to crack encryption. 

##### Review
While FTK is a very powerful tool, it offers essentially the same functionality of Autopsy and Redline, but in a much less user-friendly package. As a novice forensic investigator, I would probably never know the large differences between FTK and Autopsy, but since Autopsy is easier for me to use, I would never pick FTK unless nothing else worked.

##### Usage Notes
FTK can be installed using a `.exe` file. The license may only be good until I graduate.

FTK Imager

##### Description
>The FTK Imager is a simple but concise tool. It saves an image of a hard disk in one file or in segments that may be later on reconstructed. It calculates MD5 hash values and confirms the integrity of the data before closing the files. 

##### Review
FTK Imager is a really simple and slick program. It can be used for both live and dead acquistions which makes it incredibly valuable for obtaining images from a computer. It outputs multiple formats to then be analyzed using an image analysis program like Autopsy. 

##### Usage Notes
Be sure to bring and use a write blocker to assure that you aren't writing any data to the disk you're trying to image. Failing to do so can invalidate the evidence on that disk.

WinPrefetchView

##### Description
>WinPrefetchView is a small utility that reads the Prefetch files stored in your system and displays the information stored in them. By looking in these files, you can learn which files every application is using, and which files are loaded on Windows boot. 

##### Review
WinPrefetchView is a great, simple tool that really helps determine the root cause of suspicious activity. It helps piece together eveidence and recorded stories to identify IOCs and initial compromises of the system. Although Prefetch files can be deleted or tampered with, it's not always the most fool-proof method, it's a great starting place to start an analysis of a victim's machine.

##### Usage Notes
To use WinPrefetchView on Prefetch files obtained from a victim's machine, you need to change the source of the files by navigating to the Options Menu, selecting Advanced Options, and then change the directory of the Prefectch files.

[Redline](https://www.fireeye.com/services/freeware/redline.html)

##### Description
##### Review
##### Usage Notes

[Autopsy](https://www.sleuthkit.org/autopsy/)

##### Description
##### Review
##### Usage Notes

### Network

[Wireshark](https://www.wireshark.org/download.html)

##### Description
##### Review
##### Usage Notes

[Nmap](https://nmap.org/download.html)

##### Description
##### Review
##### Usage Notes

[Snort](https://www.snort.org/downloads)

##### Description
##### Review
##### Usage Notes

[WinPcap](https://www.winpcap.org/)

##### Description
##### Review
##### Usage Notes

### Malware

[VirusTotal](https://www.virustotal.com/)

##### Description
##### Review
##### Usage Notes

[Ghidra](https://ghidra-sre.org/)

##### Description
##### Review
##### Usage Notes

## Linux

### Memory

[Rekall](http://www.rekall-forensic.com/)

##### Description
##### Review
##### Usage Notes

[Volatility](https://github.com/volatilityfoundation/volatility)

##### Description
##### Review
##### Usage Notes

[LiME](https://github.com/504ensicsLabs/LiME)

##### Description
##### Review
##### Usage Notes

### Host

[Autopsy](https://www.sleuthkit.org/autopsy/)

##### Description
##### Review
##### Usage Notes

### Network

[Netcat](http://netcat.sourceforge.net/)

##### Description
##### Review
##### Usage Notes

[Wireshark](https://www.wireshark.org/download.html)

##### Description
##### Review
##### Usage Notes

[Nmap](https://nmap.org/download.html)

##### Description
##### Review
##### Usage Notes

[Snort](https://www.snort.org/downloads)

##### Description
##### Review
##### Usage Notes

[Zeek/Bro](https://www.zeek.org/download/index.html)

##### Description
##### Review
##### Usage Notes

### Malware

[VirusTotal](https://www.virustotal.com/)

##### Description
##### Review
##### Usage Notes

[Ghidra](https://ghidra-sre.org/)

##### Description
##### Review
##### Usage Notes

## Mac

### Memory

[Rekall](http://www.rekall-forensic.com/)

##### Description
##### Review
##### Usage Notes
OSXPMem

[Volatility](https://github.com/volatilityfoundation/volatility)

##### Description
##### Review
##### Usage Notes

### Host

[Autopsy](https://www.sleuthkit.org/autopsy/)

##### Description
##### Review
##### Usage Notes

### Network

[Netcat](http://netcat.sourceforge.net/)

##### Description
##### Review
##### Usage Notes

[Wireshark](https://www.wireshark.org/download.html)

##### Description
##### Review
##### Usage Notes

[Nmap](https://nmap.org/download.html)

##### Description
##### Review
##### Usage Notes

Snort

```shell
brew install snort
```

##### Description
##### Review
##### Usage Notes

[Zeek/Bro](https://www.zeek.org/download/index.html)

##### Description
##### Review
##### Usage Notes

### Malware

[VirusTotal](https://www.virustotal.com/)

##### Description
##### Review
##### Usage Notes

[Ghidra](https://ghidra-sre.org/)

##### Description
##### Review
##### Usage Notes
