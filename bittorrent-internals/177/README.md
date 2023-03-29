Understanding the Torrent File Format and Bencoding
===


A torrent file is an independent session of transfer. To distribute a file, say an Ubuntu image, we would create a torrent holding the meta information about it while the actual content is split into pieces and distributed in the network.

## Lifecycle of a Torrent

Torrent is alive so long as there is at least a seeder, seeding the pieces in the network. Once all the nodes who can share the pieces have left the network, the download of the network stops, and the torrent ends until a new seeder pops up.

## What torrent file holds

The `.torrent` file holds all critical meta yet static information about the content, like

- `announce` - holds the URL of the tracker
- `created by` - name and version of the program who created it
- `creation date` - time at which the torrent was created
- `encoding` - encoding of the strings in `info` dictionary
- `comment` - some additional comments
- `info` - a dictionary that describes files in the torrent

The `info` dictionary holds the information about the file that is being shared through the torrent. If the torrent is about the Ubuntu image, it will hold info like `name`, `length`, and `md5sum` of the actual file.

Given that the file is split into equal-length pieces, the `info` dictionary also holds

- `pieces` - SHA1 of every piece of the file concatenated
- `piece length` - number of bytes in each piece

This information is used in identifying and fetching pieces from the network.

## Bencoding

Torrent files are encoded with a custom encoding called Bencoding. It supports data types such as Strings, Integers, List, and Dictionaries (which can only hold string keys).

Strings are encoded as `<length>:<string>`. Hence, a string `arpit` will be encoded as `5:arpit`.

Integers are encoded as `i<integer>e`. Hence, an integer `10` will be encoded as `i10e`.

Lists are encoded as `l<becoded values>e`. Hence, the list `["a","b", 1 ]` will be encoded as `l1:a1:bi1e1`.

Dictionaries are encoded as `d<key1><value1><key2><value2>e`. Hence, a dictionary `{"a": 1, "b": 2}` will be encoded as `d1:ai1e1:bi2ee`.
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![Understanding the Torrent File Format and Bencoding](https://i.ytimg.com/vi/tHT94dSMwKw/mqdefault.jpg)](https://www.youtube.com/watch?v=tHT94dSMwKw)

System Design for Experienced Engineers: https://arpitbhayani.me/masterclass
Become a member for exclusive in-depth videos: https://www.youtube.com/c/ArpitBhayani/join
Redis Internals: https://arpitbhayani.me/redis

To download or upload any file from the Torrent network, we need a .torrent file. But what exactly is this file?

In this 2nd video of the BitTorrent Internals series, we take a detailed look into the .torrent file and understand its lifecycle, what information it holds, and the encoding it uses to structure the data.

Outline:

00:00 Agenda
02:27 Torrent File and its Lifecycle
04:33 What is in the .torrent file?
13:33 Bencoding

GitHub Repository: https://github.com/relogX/retorrent

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/13TaIK98n1SpWTLfPVfmygYVMUCyMncbr/view?usp=sharing)
 - Listen to this on the go on [Spotify](https://open.spotify.com/show/7qMoamm2iZQrsPVm6IQLoD)

# Arpit's System Design Masterclass

> A masterclass that helps you become great at designing _scalable_, _fault-tolerant_, and _highly available_ systems.

## The Program

This is a prime and intermediate-level cohort-based course aimed at providing an exclusive and crisp learning experience. The program will cover most of the topics under System Design and Software Architecture including but not limited to - _Architecting Social Networks_, _Building Storage Engines_ and, _Designing High Throughput Systems_.

The program will have a blend of Live Classes happening on Weekends, and 1:1 Mentorship sessions. The program is designed to be intense and crisp to accelerate the overall learning. We tackle every system from the [First Principles](https://en.wikipedia.org/wiki/First_principle) and build the solid foundation to architect any system in the future.


## Highlights

 - The course has been taken up by __500+__ people, spanning __9__ countries.
 - People from companies like Tesla, Amazon, Microsoft, Google, Yelp, Github, Flipkart, Practo, Grab, PayPal, and many more, have taken up this course.


## Hi, I'm Arpit Bhayani 👋

<img width="256px" src="https://arpitbhayani.me/static/img/arpit.jpg" />

In my last **~10** years of experience, I have worked at **D. E. Shaw**, **Practo**, **Amazon**, and **Unacademy**; and have built systems, services, and platforms that scaled to billions.

Post my masters in CSE from **IIIT Hyderabad** I joined D. E. Shaw for a short stint of 2 months, before moving to Practo and working there as a **Platform Engineer**, building and owning close to 8 different microservices. Post Practo I worked at Amazon on their primary mission-critical E-Commerce Database and built **Data Pipelines** that cold tiered the stale data.

After quitting Amazon in 2018, I joined Unacademy as their first **Technical Architect** and there I designed, built, managed, and scaled services like _Search_, _Notification_, _Logging_, _Deployment Engine_, and many more. I have now transitioned into the role of a Sr. Engineering Manager, leading the Site Reliability vertical.

I also run a YouTube channel [#AsliEngineering](https://www.youtube.com/c/ArpitBhayani) where I post 3 videos every week spanning topics like System Design, Distributed Systems, Microservices, and any interesting CS concept in general.

You can find details about upcoming cohort 👇‍ Hope to see you soon there.

<center>
<a target="_blank" href="https://arpitbhayani.me/masterclass">
<img src="https://user-images.githubusercontent.com/4745789/137859181-d4499cf4-ce65-4466-8b88-a078ece0f081.PNG" width="300px" />
</a>
</center>