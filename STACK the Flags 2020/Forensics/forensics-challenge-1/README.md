# Walking down a colourful memory lane
**Points: 1000**

Prompt: "We are trying to find out how did our machine get infected. What did the user do?"

File(s) provided: "[forensics-challeng-1.mem](forensics-challeng-1.mem)"

Hint: "Understanding Windows memory"

Upon obtaining the memory image, the first thing that I did was to identify the OS in which this memory image was taken from. This is crucial because every OS does its memory addressing differently (even between versions).

I was running a native version of volatility on Kali Linux, but you could just make use of the Python version, link can be found here:
> volatility -f forensics-challenge-1.mem kdbgscan

> volatility -f forensics-challenge-1.mem imageinfo

I usually prefer the kdbgscan results as they tend to


Opening the file in Microsoft Word would give us an error.
Peering into the file using Word, we see the PNG file signature at the top.
![Error](word.png)

To further confirm this, we can run this in terminal:
> file documents.doc
![file command](file.png)

Now, renaming the file as documents.png instead, opening the image, we get the flag:
![documents.png](documents.png)
> wh{4lway5_h4s_b3en}
