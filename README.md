# Twitch Polling Tool

A Twitch polling tool bot and poll visualization overlay for custom polls.

## Integration into OBS

Download the index.html and style.css and make sure that you keep them in the same folder.

First, add the overlay by adding a browser source in OBS. The URL needs to be file-based (not http-based). **Don't** check "Local file" and enter this into the URL field and replace the path accordingly to wherever you put the downloaded files:

```
file:///path/to/index.html
```

You also must append a parameter to the URL to specify your Twitch channel name.

So, for example if your twitch channel name is XYZ:

```
file:///path/to/index.html?channel=XYZ
```

If you don't want the default position (top left) you can specify append another parameter to the URL to change this. The following URL puts the overlay into the bottom right:

```
file:///path/to/index.html?channel=XYZ&positon=br
```

Replace the `br` with any corner you like. These are the supported options:

- `tl`: top left (default)
- `tr`: top right
- `br`: bottom right
- `bl`: bottom left

## Commands

The chat commands to start and edit polls are only available to the broadcaster.

### Starting a Poll

There are different ways to start a poll:

`!poll`: Starts a poll with just two options named 1 and 2.

`!poll 3`: Starts a poll with three options named 1, 2, 3. (Up to 9 options are supported).

`!poll "do you like cats?" "do you like dogs?" "do you like both?"`: Starts a poll with three named options. These names will appear next ot the number.

### Stopping a Poll

`!pollstop`

This will stop the currently active poll in its current state and highlights the winning option. If several options have a draw they will be highlighted together.

### Resuming a Poll

`!pollresume`

This will resume the currently stopped, but still visible poll.

### Ending a Poll

`!pollend`

This completely ends the poll and throws away the results. You can't recover the results after.
