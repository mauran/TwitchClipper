﻿# TwitchClipper
TwitchClipper is a .NET 5.0 cross platform compatible application, made to download https://twitch.tv clips. Downloading is done via [youtube-dl](https://yt-dl.org/), which will automatically be downloaded and saved in the project's folder.

Head over to [the Wiki](https://github.com/mortenmoulder/TwitchClipper/wiki) to find some documentation on various topics.

## Features
* [Custom save path expressions](https://github.com/mortenmoulder/TwitchClipper/wiki/Custom-save-expressions)
  * Allows you to save a clip in the exact location you want AND [in your own language](https://github.com/mortenmoulder/TwitchClipper/wiki/Language-support)
* Save ALL clips (no limit)
  * Many clip downloaders out there, can only download about 1000 clips before being throttled by Twitch. TwitchClipper has bypassed that limitation!
* Skip download if a file with the same name exists

## Installation
Head over to the Wiki to find the installation steps (IT'S REALLY EASY): https://github.com/mortenmoulder/TwitchClipper/wiki/Installation

## Configuration
`appsettings.json` contains all the things you need to change, in order to start using TwitchClipper.

There's a section called `TwitchConfiguration` you need to modify:

```json
"TwitchConfiguration": {
  "ClientID": "CLIENT_ID_GOES_HERE",
  "ClientSecret": "CLIENT_SECRET_GOES_HERE",
  "DownloadThreads": 5
}
```

1. Go to https://dev.twitch.tv/console and create your app
2. Go to your app and find the Client ID and generate a new secret
3. Replace `CLIENT_ID_GOES_HERE` and `CLIENT_SECRET_GOES_HERE` with your newly copied values

`DownloadThreads` spawns x amount of youtube-dl instances. The higher the number, the faster your download will be. I do not recommend going over 10, as you might get throttled by Twitch.

Optionally you can also modify the `Download` section, if you want to customize where your clips are saved:

```json
"Download": {
  "SavePathExpression": "/{broadcaster_name}/{yyyy}-{MM}-{dd}/{id}.mp4",
  "Locale": "en-US"
}
```

## Few minor things
This is my first published .NET app. I'm a web developer, so please bear 🐻 with me.

1. If you ever need to get the new version of this, you simply need to do `git pull` followed by the long `dotnet publish .....` command.
2. Edit appsettings.json BEFORE you run the `dotnet build/publish` commands. The file will automatically get copied to the `publish` folder
3. When the authentication token has been generated, it will be stored in the new appsettings.json file in the publish folder (which will be overwritten next time you build)

## TODO:
1. ~~Custom input on how you want the folder structure to be. Currently it's USERNAME\YEAR\MONTH\DAY\CLIP_TITLE (aka "slug")~~
2. Clean up some of the messy "if linux or osx then"-code
3. Make the -u argument optional, and introduce some kind of flag you can set, that downloads from a list of users in appsettings.json
4. Error handling (pff works on my machine)
5. DOCKER CONTAINER
6. ~~someone please see if it works on osx please~~ THANK YOU @mauran
7. ~~Check if file exists before overwriting it (waste of time)~~
8. Somehow allow the user to determine how many videos they want (filtering, basically). Not everyone wants every video
9. ~~Refactor to Helix API instead of Kraken, which apparently was newer~~
10. Make releases!
