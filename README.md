# Twitch Polling Tool

A Twitch polling tool bot and poll visualization overlay for custom polls.

## Setup

### Running on glitch.com

You can import this repository on glitch.com to automatically have it editable and hosted at the same time.

1. Create an account on glitch.com
2. On your dashboard look for "Import from Github"
3. Supply the GitHub URL of this repository where it says "Paste URL here"
4. Hit import and wait until your imported project is opened
5. In the code editor's left pane select the `package.json` file
6. Add a property to the configuration for glitch, so that it creates a production build when you close the editor

```json
  ...
  "devDependencies": {
    ...
  },
  // Add the following:
  "glitch": {
    "projectType": "generated_static"
  }
```

### Running Locally

With `npm start` you open up a dev server under `http://localhost:3000`.

The tool runs in the browser `http://localhost:3000?channel=XYZ` in a browser and supports Hot Module Reloading, which means that any changes made in code are directly visible.

### Running On a Web Server

With `npm build` the bundle is built into the build folder which can then be served statically by any web server or service that serves static files.

## Integration into OBS

Use one of the choices above to set up the poll tool. Let's say you have it working under glitch.com with the url `https://rando-url-soup.glitch.me`. This is how you integrate it into OBS.

Go to OBS and add a browser source. As the URL you input:

```
https://rando-url-soup.glitch.me?channel=XYZ
```

Substitute XYZ with your channel name.

Make sure you adjust the values for width and height to:

```
width: 1920
height: 1080
```

If you don't want the poll to be in the default position (top left) you can append another parameter to the URL to change this. The following URL puts the overlay into the bottom right:

```
https://rando-url-soup.glitch.me?channel=XYZ&positon=br
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

`!poll`: starts a poll with just two options named 1 and 2.

<img width="1920" alt="Bildschirmfoto 2022-07-30 um 22 08 15" src="https://user-images.githubusercontent.com/94025590/181994769-7bb71d57-cb0a-4d26-91c1-7828597e3489.png">

`!poll 3`: starts a poll with three options named 1, 2, 3. (Up to 9 options are supported).

<img width="1920" alt="Bildschirmfoto 2022-07-30 um 22 08 42" src="https://user-images.githubusercontent.com/94025590/181994778-fa08a89b-84e2-494e-a918-37866663bbc5.png">

`!poll "what kind of person are you? "cat person?" "dog person?" "why not both?"`: starts a poll with a title (the first text) and three named options and a title (everything after the first text). These option names will appear next to the option numbers.

<img width="1920" alt="Bildschirmfoto 2022-07-30 um 22 09 59" src="https://user-images.githubusercontent.com/94025590/181994811-878d4d6b-5c9d-487e-b34f-63c2d6cff14c.png">

`!poll "" "cat person?" "dog person?" "why not both?"`: leaves out the title (which will default to "Poll") and supplies the same three options:

<img width="1920" alt="Bildschirmfoto 2022-07-30 um 22 10 20" src="https://user-images.githubusercontent.com/94025590/181994877-82a22432-5799-4ffd-9995-d29a1fed0f82.png">

### Changing the Poll Title

`!polltitle "New Poll Title"`

This will change the poll title of the currently active poll to "New Poll Title".

### Stopping a Poll

`!pollstop`

This will stop the currently active poll in its current state and highlights the winning option. If several options have a draw they will be highlighted together.

<img width="1920" alt="Bildschirmfoto 2022-07-30 um 22 10 43" src="https://user-images.githubusercontent.com/94025590/181994884-358fb293-2daa-4406-93f9-efd0bb93ab3a.png">
<img width="1920" alt="Bildschirmfoto 2022-07-30 um 22 11 21" src="https://user-images.githubusercontent.com/94025590/181994887-30a27146-d739-4b77-8be2-e4b52dc968ee.png">

### Resuming a Poll

`!pollresume`

This will resume the currently stopped, but still visible poll.

### Ending a Poll

`!pollend`

This completely ends the poll and throws away the results. You can't recover the results after.

## How Votes Work

When a poll is active any number that is put into chat counts as a vote by that user. Following rules apply:

- A number is only counted when it is a valid option number
- A number is only counted when the message starts with that number (optionally followed by a space and arbitrary other text).
- A user can change their vote to another number by inputting another valid number
- With inputting 0 the user can withdraw their vote
