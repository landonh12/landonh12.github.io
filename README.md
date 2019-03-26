# Squeak

A game for Game Design at Mississippi State for the Spring 2019 semester.
This game is super simple. It is made using JavaScript and a simple canvas object. There are no art assets, all art is done programatically in JavaScript.

## Gameplay

Press start, and use your mouse to hover over the circles. They will explode and squeak. When all the circles are exploded, the game will add your score to the leaderboard. The leaderboard does not save, so get all of your friends to play without refreshing the page.

## Issues

When creating this game, I originally wanted to make it very annoying but also addicting. Getting the highest score possible was the addicting part, but the squak was a funny touch. I tried to make the game play the squeak sound every time you destroyed a circle, but loading 100 audio objects and playing them each time a circle exploded led to the game getting very bogged down in performance. So I had to resort to making one audio object and playing it each time, but I couldn't find a way to cancel the sound on each new destruction.

Also, dictionaries in JavaScript are weird, and I couldn't get them to work. I wanted to use them for the leaderboard so a name could be attached to a score, but with limited time, it was on low priority. I thought about writing scores to a CSV and reading them back from the web server for a "hiscores" page, but that was also weird to do with JavaScript, and again, I had limited time.

## Resources 

I used this mozilla resource to get started with moving objects on a canvas in JavaScript. I only used the first few pages. I created a class for balls, a class for the "destroyer", and all of the logic for the game.

https://developer.mozilla.org/en-US/docs/Games/Tutorials/2D_Breakout_game_pure_JavaScript