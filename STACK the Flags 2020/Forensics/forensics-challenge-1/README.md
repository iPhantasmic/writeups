# Walking down a colourful memory lane
**Points: 1000**

Prompt: "We are trying to find out how did our machine get infected. What did the user do?"

File(s) provided: "[forensics-challenge-1.mem](forensics-challenge-1.mem)"

Hint: "Understanding Windows memory"

Upon obtaining the memory image, the first thing that I did was to identify the OS in which this memory image was taken from. This is crucial because every OS does its memory addressing differently (even between versions). Volatility is the go-to tool for memory analysis, this is what we will be using to perform this investigation.

I was running a native version of volatility on Kali Linux, but you could just make use of the Python version (vol.py), it would work just as well.
> volatility -f forensics-challenge-1.mem kdbgscan

> volatility -f forensics-challenge-1.mem imageinfo

My personal SOP is to just run imageinfo since it performs a [kdbgscan](kdbgscan.txt) as well. From the results of [imageinfo](imageinfo.txt), Win7SP1x64 is the first profile that is given, the list provided usually tends to be accurate and we can check this by simply running pslist. In the event where no processes show up, the profile is likely to be incorrect.

From here on, every command would be preceded by:
> volatility -f forensics-challenge-1.mem --profile==Win7SP1x64

Since the prompt mentioned the user doing something, I first ran pslist to obtain all running processes in memory. Taking a quick look through [pslist](pslist.txt), there didn't seem to be any malicious processes off the bat. Although there was a significant number of chrome tabs open (he must've been busy with STACK the Flags 2020 as well). To better visualise the parent-child process relationships, we can run pstree. The output of [pstree](pstree.txt) shows us that there is a large number of

Opening the file in Microsoft Word would give us an error.
Peering into the file using Word, we see the PNG file signature at the top.
![Error](word.png)

To further confirm this, we can run this in terminal:
> file documents.doc
![file command](file.png)

Now, renaming the file as documents.png instead, opening the image, we get the flag:
![documents.png](documents.png)
> wh{4lway5_h4s_b3en}
