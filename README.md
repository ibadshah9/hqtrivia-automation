# hqtrivia-automation (WIP)
I vaguely wondered about the HQ trivia game and automating to get an edge in the game since there is nothing stopping you from googling for answers. Why not automate it in effort to learn? Well here's my attempt...

Note using this during live game would break HQ's terms of service. So if you want to play around with it like I did, just take snapshots of the question and use after game. DO NOT USE TO CHEAT!!! Made for educational purposes only!!!

# Work Flow
1. Capture source image either via quicktime player (recommended) or webcam (untested). If using quicktime you can do a movie recording without actually recording. Just hit the drop down arrow by the record button to select iPhone as source (iPhone must be connected by wire).

2. Multiple OCR engines will attempt to read the text off image. Currently supporting Google Tesseract OCR (free/open source) or Google Vision API (free but requires billing account and has limits). Note that Vision API is generally better.

3. Text is parsed into question and answers. The answers are then searched wikipedia, google search, multiple dictionaries and synonyms are looked up too. NOTE: More will be added soon. Finally, searches that have more relevancy with the question are scored higher. The answer that scores the highest is shown. NOTE: All of this is done in a multiprocessing pool to speed up results.

4. Display the results on screen as answers are being looked up.

# Installation
Use python 3.6 and take notice of the modules used in the python file. In particular the packages used are...

* Pillow - Image manipulation
* numpy - More advanced image manipulation
* PyObjC - AppleScript for taking screenshot
* opencv-contrib-python - WebCam for taking screenshot
* wikipediaapi - Wikipedia searches
* vocabulary - Dictionary and synonyms searches
* pytesseract - Google's free/open source OCR (requires seperate installtion)
* google-cloud-vision - Google's commercial OCR (free also but with limits and additional setup)
* nltk - local dictionary
* beautifulsoup4 - parse google searches

*Oversimplified steps*
1. Install python 3.6
2. Install above packages
    * `pip3 install -r requirements.txt`
3. For nltk run *python3 -m nltk.downloader all*

# Usage
Simply execute script with the right options...

```
$ python3 hqtrivia-automation.py -h
usage: hqtrivia-automation.py [-h] [-q | -w | -i INPUT] [-v] [-V]

Automate searching for answers in HQ Trivia

optional arguments:
  -h, --help            show this help message and exit
  -q, --quicktime       Use quicktime to capture source image
  -w, --webcam          Use webcam to capture source image
  -i INPUT, --input INPUT
                        Use image provided instead of capturing
  -v, --verbose         Spit out debug information
  -V, --version         Version of script
```
NOTE: Have to select -q, -w or use -i
