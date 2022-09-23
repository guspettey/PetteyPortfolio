---
layout: post
title:  "Controlling OneDrive Syncing by Command Line"
date:   2022-07-10 12:30:00 +0000
tags: [PhD, Python, File Management, particleVirtualization, OneDrive]
---

During my quest for [Virtualizing many grains of sand](https://www.pettey.co.uk/devprocesspart3/) I found myself needing to distribute my processing code to operate on multiple machines, in order to overcome memory restraints.
This raises the inevitable consequence of needing a central repository of files that can be accessed by multiple machines. 
Due to University of Nottingham policy to remove shared network drives and move all file storage onto office365, this topic is far more troublesome than it has been previously, as files need to be downloaded via OneDrive to the local machine for processing.
Downloading the full 200GB of data to each machine without OneDrive could have been done.
However, this lacks the advantage that any analysis can be shared between machines and furthermore,  this method would require manually re-uploading processed data.

Whilst OneDrive is easy to interact with via Windows File Explorer/MacOS Finder, it leaves a lot to be desired when interacting via the command line.
[A help document does explain the functionality but is not well publicised. ](https://learn.microsoft.com/en-us/OneDrive/files-on-demand-windows)
To simplify this process, [a gist is available on my github](https://gist.github.com/Gustafferson/fb6b25f599d25561f53b691097efa18d) containing two python functions for pinning (download) and unpinning (offload) files from a OneDrive or Sharepoint hosted directory, by a subprocess call.
The directories first need to be synced to your machine, *and if on MacOS* the path to the OneDrive executable needs to be given in the python file.

<script src="https://gist.github.com/Gustafferson/fb6b25f599d25561f53b691097efa18d.js"></script>

Here outputs of the subprocess command are redirected to DEVNULL but revealing the outputs will return the exit code on MacOS.
Code 0 means the operation has been successful.

Running these commands in advance of operating on the downloaded files has a great impact on speed, rather than letting OneDrive download them as and when needed.
