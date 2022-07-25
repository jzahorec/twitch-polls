# Twitch Chat Overlay Base

A Twitch bot and visualization overlay for doing custom polls.

## Usage

Download the index.html and style.css and make sure that you keep them in the same folder.

First, add the overlay by adding a browser source in OBS. The URL needs to be file-based (not http-based) and looks like this:

```
file:///path/to/index.html
```

Append a parameter to the URL to specify your twitch channel name.

So, for example if your twitch channel name is XYZ and you want the normal chat mode.

```
file:///path/to/index.html?channel=XYZ
```
