# Walking down a colourful memory lane
**Points: 1000**

Prompt: "We are trying to find out how did our machine get infected. What did the user do?"

File(s) provided: "[forensics-challenge-1.mem](forensics-challenge-1.mem)"

Hint: "Understanding Windows memory"

**The outputs for commands ran can be found in the respective text files**

## My Attempt
Volatility is the go-to tool for memory analysis, this is what we will be using to perform this investigation. I was running a native version of Volatility on Kali Linux, but you could just make use of the Python version, it would work just as well.

Upon obtaining the memory image, the first thing that I did was to identify the OS in which this memory image was taken from. This is crucial because every OS does its memory addressing differently (even between some versions).

> volatility -f forensics-challenge-1.mem kdbgscan

> volatility -f forensics-challenge-1.mem imageinfo

For this, my personal SOP and preference is to run imageinfo since it performs a [kdbgscan](kdbgscan.txt) as well. From the results of [imageinfo](imageinfo.txt), Win7SP1x64 is the first profile that is given, the list provided usually tends to be accurate and we can check this by simply running pslist. In the event where no processes show up, the profile is likely to be incorrect.

From here on, every command would be preceded by:
> volatility -f forensics-challenge-1.mem --profile==Win7SP1x64

Since the prompt mentioned the user doing something, I first ran pslist to obtain all running processes in memory. Taking a quick look through [pslist](pslist.txt), there didn't seem to be any malicious processes off the bat. Although there was a significant number of chrome tabs open (he must've been busy with STACK the Flags 2020 as well).

To better visualise the parent-child process relationships, we can run pstree. The output of [pstree](pstree.txt) shows us chrome.exe opening many other child processes of chrome.exe, logically for me it would make sense to take a look at the parent process first:
> memdump -p 2904 --dump-dir=./
This gives us the memory dump for the parent process chrome.exe with pid of 2904

From the memdump, we can strings it to find any visited links and any other meaningful data:
> strings 2904.dmp

From the [output](chrome_string_dump.txt), I just searched through looking for any interesting links. This was the beginning of my downfall as I spent several hours going through various avenues to no avail. Below is a list of the commands I've ran and the rationale behind each:

1. I attempted to take a look at the notepad.exe memory dump and see if there were any text files opened in notepad that could potentially contain the flag
> memdump -p 3896 --dump-dir=./
  strings 3896.dmp | grep .txt


2. Next I took a jab at iehistory in hopes of finding any browsing history, but of course this pertains only to

TBC

## Solution From Community
At the end of the CTF, I visited the Discord channel for some spoilers to see where I went wrong, only to realise that I had everything that was necessary to find the flag.

The output of running strings (chrome_string_dump.txt) already showed us a mediafire URL at the top of the file, this is the lead necessary to find the flag. Searching for mediafire, there would eventually be a link to a .png image hosted on mediafire.
![mediafire link](mediafire.png)
[Link]()

Downloading that image would give us a  

Now, running strings on .rgb we would get the flag:
![flag.png](flag.png)
> **govtech-csg{}**

Overall, my workflow was sufficient for me to obtain the flag, but I didn't search hard enough through his Google Chrome history to be able to identify the mediafire link that contained the image to the flag.

## **Learning Resources/References:**
- My simplified workflow is as follows:
1) imageinfo
2) pslist/pstree
3) memdump interesting processes
4) Run strings on memdump
5) Repeat the process, and make use of other modules as and when potential artefacts are identified

- Andrea Fortuna's series on volatility is a good start:
[Part 1](https://www.andreafortuna.org/2017/06/25/volatility-my-own-cheatsheet-part-1-image-identification/)
[Part 2](https://www.andreafortuna.org/2017/07/03/volatility-my-own-cheatsheet-part-2-processes-and-dlls/)
[Part 3](https://www.andreafortuna.org/2017/07/10/volatility-my-own-cheatsheet-part-3-process-memory/)
