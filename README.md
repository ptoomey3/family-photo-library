I've searched high and low for some means of creating a shared family library such that my wife and I can each independently take pictures and they end up in a single library that becomes our shared "source of truth". After trialing nearly every option under the sun (at least twice) I've arrived at using Google Photo as the best solution in 2018. 

Here are the steps to setup a shared family library. The following directions assume you have access to a Mac, are not philosophically opposed to using Google services, etc. 

## How to set it up

1. Create a family gmail account (ex. house-yourlastname@gmail.com)
1. Install Google Photos on the both you and your partner’s phone and set the automatic photo upload to upload to the house-yourlastname@gmail.com account.
1. Create a new account on your local "home server" (ex. house-yourlastname)
1. Install and login to the google drive client for the house@yourlastname.com account. **Don't** do any of their photo upload nonsense. Just use the app to sync your google drive contents.
1. Go to https://photos.google.com and set the "Sync photos & videos from Google Drive” to “true”.
1. Go to https://drive.google.com and set the "Automatically put your Google Photos into a folder in My Drive” to true.
1. Install [hazel](https://www.noodlesoft.com) on your home server and add the “Google Photos” folder as a "watched folder". This folder is the one that shows up in your Google drive as a result of step 6. This folder is where all auto-uploaded photos from your phone(s) end up by default.
1. Create a folder called "Photos" inside the top level of your Google Drive folder (ex. `mkdir ~/Google\ Drive/Photos`). This is the root folder where we will store all organized photos. 
1. Install `exiftool` using homebrew `brew install exiftool`.
1. Download [these hazel rules](https://github.com/ptoomey3/family-photo-library/raw/master/google_photos.hazelrules) and add them to the "Google Photos" that is being watched as of step 7. These rules will automatically move all auto-uploaded photos out of the “Google Photos” folder in Google Drive and into the "Photos" folder structure we created in step 8 (Ex. “Google Drive/Photos/2018/11/2018-11-25-1234.jpg”). Because of step 5, the photos we move into our own folder structure will show up on https://photos.google.com.
1. Whenever you want to import photos from non-smartphone devices (DSLR, etc), copy the photos into the "Google Photos" folder you are watching with hazel. This will cause hazel to process these photos the same as auto-uplaoded photos. 
1. Done - you have a pretty good shared family library. All family members can view all photos using the google photos app OR by visiting https://photos.google.com. And, any management (deletes, etc) are propagated to Google Drive. For example, I’ll triage on https://photos.google.com and all deleted photos end up n the trash can of my iMac by the time I happen to check.

## Why I chose this setup:

1. I have a family and whatever I chose had to work for the whole family without jumping through manual copying at home. This basically nixes Apple photos, as they haven’t yet figured out we have families.
1. The only graceful way I’ve found to have a family library is to have spouses share an account. You could do that with an iCloud account, but there are lots of downsides to that. Google apps support multiple account gracefully, which allows you to be logged into a different account for Google Photos vs. Gmail (or whatever).
1. Most photo management solutions require you go sit down on the “shared family computer” to manage them. Google Photos bootstrapped off of using Google Drive lets you manage photos from anywhere (your phone, your spouse’s phone, the website, etc). The changes are synced back to Google Drive and back to your “source of truth” on your home server, Synology, etc.
1. The above solution only relies on the home server for sake of moving photos around to the folder structure of your liking. Even if your machine is turned off for a week, all your photos end up in the family library pretty quickly. Whenever you happen to start the server again, all the photos sitting in the “Google Photos” folder will then get organized into your preferred folder structure. This is appealing, as I didn’t like any solution I tried that relied on a server being up 24/7 to have all photos show up in the family library.
