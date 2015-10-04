# pyFlickrDownloader - 'Apollo' Edition

## Intro

This is a Python 3.x script that extracts a list of direct links to high-resolution photos from NASA's Apollo mission Flickr photostream.

As soon as NASA released all the images, I wanted to download them all. Trying numerous "Flickr downloaders" was a terrible experience so a wrote my own script in an hour. Decided to publish it, so I refined it a bit and here it is!

## How to use it

You need Python 3.x for any platform, Windows, OS X and Linux should all works. (I tested only on Debian.)

Download the script and just run it with `python3 pyApolloDL.py`

It creates a file with a list of direct links which you then give to wget like this: `wget -i photolinks.lst`

Wget downloads all photos in the same folder and voila!


## Modification

If you want to modify and adapt the script for other Flickr downloads, keep in mind that the script only downloads photos in "Original" size from Flickr, and only if the uploader has enabled downloads (the latter has not been tested, to be honest, but I suppose that's the case).

If you've got Python skillz, you can modify the script to download different sizes, and to circumvent disabled downloads, but it'll take you time.

**NOTE: ** This script has only been tested with photostreams that span 10+ pages long. `getPageCount()` function relies on those three dots (`...`) between pages at the bottom of the photostream to count the pages properly. If that's missing, you have to modify the function or force it to return a custom, manually entered number of pages.


### Algorithm

The script works like this:

 - Send a GET request and download the HTML from the MAIN_URL variable.
 - Parse the HTML to extract the number of pages from it.
 - Repeat the following loop for each page:
 	- Download the HTML of the page
 	- Parse it to extract direct links to "Original"-sized images
 	- Append links to a global variable `finalLinksList`
 - Once done, write all links to a file whose filename is set by LINKS_LIST_FILENAME

### Contribute

If you give enough of a shit, feel free to submit patches, I'm happy to accept them as I probably won't be improving this script much unless I need it again for something.
