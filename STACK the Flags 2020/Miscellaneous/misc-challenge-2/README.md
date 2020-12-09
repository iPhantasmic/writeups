# Sounds of freedom!
**Points: 1000**

Prompt: In a recent raid on a suspected COViD hideout, we found this video in a thumbdrive on-site. We are not sure what this video signifies but we suspect COViD's henchmen might be surveying a potential target site for a biological bomb. We believe that the attack may happen soon. We need your help to identify the water body in this video! This will be a starting point for us to do an area sweep of the vicinity!

Flag Format: govtech-csg{postal_code}

File(s) provided: "[osint-challenge-7.mp4](osint-challenge-7.mp4)"

## My Attempt
We are provided with a video, showcasing the location of COViD's potential bomb site. The end goal is to identify the water body as shown in the second half of the video.

There really isn't much to go off, especially since there is quite a number of water bodies in Singapore. The limited view of the water body makes judging its size difficult. Enumerating all water bodies no longer becomes a viable option..

One thing that stuck out to me was the audio, it sounded like a rumbling that many would find annoying as the National Day Parade (NDP) rehearsals take place annually. This is supported by the clue in the title of the challenge, "Sounds of freedom".. Perhaps we could look for water bodies nearby airbases.

From our results, we can effectively eliminate the West side of Singapore as there are no airbases with water bodies nearby.
![airbase](airbase.png) To the keen-eyed, we would need to find a water body with plenty of greenery nearby, alongside some residential areas, as seen in the background of the video. This would then eliminate Sembawang Air Base and Changi Air Base from our list of candidates.

This leaves us with Paya Lebar Air Base, the last of the 4 airbases in Singapore. Zooming in, we can see that there is Punggol Park just above, and to confirm our findings, we can make use of Google Street View to identify any landmarks. The following image provides a point of view that matches many of the features in the video. ![features](features.png) We can see the green and white residential buildings, alongside the red-tiled roofs with plenty of greenery surrounding the water body.

To further confirm our findings, we can identify the residential building in which the video was taken from. Using Google Maps, we just need to identify the bus stop right beside Punggol Park, since there was one at the bottom of the building in the video. ![satellite](satellite.png) ![street1](streetview1.png) ![street2](streetview2.png)
From these images, we can see how the architectural features match up exactly with our video.

Hence, we can get our flag as shown below.
![flag](flag.png)
The flag is:
> **govtech-csg{538768}**
