# youtubeDownloader
[![Made With - Python](https://img.shields.io/badge/Made_With-Python-2ea44f?style=for-the-badge&logo=python)](https://python.org)
---
youtubeDownloader is a program codded in Python that via a graphical interface allows you to download YouTube videos to any folder you want in your computer.

### Code Structure
My code is composed of the following parts:

1. Import the required libraries:
```py
import tkinter as tk
from tkinter import *
from pytube import YouTube
from tkinter import filedialog, messagebox
```

2. Create a function to create the app box:
```py
# DESCRIPTION: This function creates the box for our application.
def createBox():
    root.geometry("600x120")
    root.resizable(False, False)
    root.title("YouTube Downloader by Eur1p3des")
    root.config(background="#000000")

```
3. Create the function that creates the necessary widgets to run the app properly:
```py
# DESCRIPTION: This function creates all the widgets user in the app.
def createWidgets():
    ################################################################
    #Create the box that contains the message To insert the youtube link
    link_label = Label(root, text="Youtube Video URL: ", bg="#E8D579")
    link_label.grid(row=1, column=0, pady=5, padx=5)
    #Create the entry box where you can input your link
    root.link_text = Entry(root, width=60, textvariable=video_link)
    root.link_text.grid(row=1, column=1, pady=5, padx=5)
    ################################################################

    ################################################################
    #Create the box that contains the message To insert the path where you want to save the video
    destination_label = Label(root, text="Destination: ", bg="#E8D579")
    destination_label.grid(row=2, column=0, pady=5, padx=5)
    #Create the entry box where you can input the path where you want to save the video
    root.destination_text = Entry(root, width=60, textvariable=destination_link)
    root.destination_text.grid(row=2, column=1, pady=5, padx=5)
    #If you don't know the full path, the button created here calls the function browse which opens your file manager so you can sellect
    # the folder.
    browse_but = Button(root, text="Browse", command=browse, width=10, bg="#05E8E0")
    browse_but.grid(row=2, column=2, pady=1,padx=1)
    ################################################################

    ################################################################
    #Create the download button
    download_but = Button(root, text="Download", command=download_video, width=25, bg="#05E8E0")
    download_but.grid(row=3, column=1, pady=3, padx=3)
```
4. We now shall create the function to open the file manager when browse button is clicked:
```py
# DESCRIPTION: This function opens the file manager so you can choose your destination folder
def browse():
    # Opens the file manager where you can select the folder
    download_dir = filedialog.askdirectory(initialdir="Your Directory Path")
    # Inputs the folder path you have chosen into the destination box
    destination_link.set(download_dir)
```
5. We must now create the function that will download the video when the "Download" button is clicked:
```py
# DESCRIPTION: This function downloads the video.
def download_video():
    #Grab the youtube link and stores it in the url parameter
    url = video_link.get()
    #Grab the folder path you have chosen and save it in the folder parameter
    folder = destination_link.get()

    #Search for the video in YouTube with the url parameter
    get_video = YouTube(url)
    #Finds the highest resolution of the video and stores the link in the get_streams parameter.
    get_streams = get_video.streams.get_highest_resolution()
    #Downloads the video stored in get_streams to the folder path you have chosen.
    get_streams.download(folder)

    #If the video has been downloaded successfully, a popup window appears indicatingthat the video has been downloaded.
    messagebox.showinfo("Success!!", "Download Successful! You will find your video at\n"+folder)
```
5. Finally, we can call all the functions so that the program runs:
```py
################################################################
#                    MAIN PART OF THE CODE                     #
################################################################
root = tk.Tk()
createBox()
video_link = StringVar()
destination_link = StringVar()
createWidgets()
root.mainloop()
```
