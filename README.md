# MTG Autoproxy
Use Photoshop scripting to easily create custom high-quality Magic proxies for casual play.
*NOTE*: If you downloaded the templates prior to the 9th of October 2019, you'll need to redownload them to use the latest version of this tool.

# Examples
[Video demonstration](https://www.youtube.com/watch?v=jSuH7CY8HIM)

Original digital render example
![img1](https://i.imgur.com/p6jJ8Mu.jpg)

Example printed through http://makeplayingcards.com
![img2](https://i.imgur.com/fP9S81O.jpg)

# What You'll Need
* A copy of Photoshop. I tested the system using CS5 and CC 2018, but other versions may work as well.
* [The Photoshop templates](https://drive.google.com/open?id=1s-mVBKkMzJMhzxrfjb8SiJms1EEVvoxq) (download `automated.zip`)
* The following fonts:
  * [Beleren Smallcaps, MPlantin and MPlantin-Italics](https://github.com/magarena/magarena/tree/master/resources/cardbuilder/fonts) and [Beleren2016](https://magic.wizards.com/sites/all/themes/wiz_mtg/fonts/Beleren/Beleren2016-Bold.ttf), for most text
  * My custom Magic symbols font NDPMTG, as well as MTG2016, both included in the repo.
  * [Keyrune](https://andrewgioia.github.io/Keyrune/index.html), for the expansion symbol.
 * [json2.js](https://github.com/douglascrockford/JSON-js), included but you may need to download a more recent version.
 
 As well as the Python packages (I tested the script using Python 3.6.3):
 * json
 * Scrython

# Install / Usage Guide
* Clone to a folder of your choice, referred to as the *working directory*.
* Install the included font and the other fonts specified above.
* Download the Photoshop templates and move them into the `templates` folder of the working directory.
* Create a folder called `art` in the working directory, and another called `out`. Create a folder called `border` inside `out`.
* Move all of your card artwork to the `art` folder. File names should be structured as `<CARDNAME> (<ARTIST NAME>).jpg`.
* Run the script `proxyAll` to render each card in the `art` folder, and store the results in the `out` folder. `proxyTarget` does the same but only for a specific art image.
* Run the script `borderifyAll` to pad each card render with a black border, such that it's ready to order through sites like http://makeplayingcards.com, and store the results in the `border` folder inside the `out` folder. `borderifyTarget` does the same but only for a specific render.
* Toggle comments on the first couple of lines of `proxy.jsx` to switch between the normal template and box topper template. Box topper renders don't need to be borderified.

# FAQ
Photoshop scripting works within an outdated version of JavaScript and has more than its share of idiosyncrasies. There are unfortunately bugs that don't occur on my system and that I can't recreate, but others have found ways to fix them.
* *When I try to run the script, I get "Error: File or folder does not exist." Line 9: $.evalFile(filePath + ...).* So far it seems like the way to fix this issue is to hardcode the path to your directory in each script, unfortunately. Dynamically finding the filepath works perfectly on my system so I'm not sure exactly how to debug it for others.
* *When I render a card, the artwork is twice as big as it should be.* Hop into `frame.jsx` and scroll down to the bottom. In the `frame()` function, there's a line that looks something like `var percentageToScale = 100 * (Math.max( ... ));`. Change the number 100 to 50 here and that typically fixes it.
* *My set symbols don't have the proper gradient to them.* I haven't found a fix for this yet, but it's in the pipeline.
* *I want to change the set symbol to something else.* Head over to https://andrewgioia.github.io/Keyrune/cheatsheet.html - you can use any of these symbols for the set symbol for your cards. Copy the text of the symbol you want on the cheatsheet, then hop into `proxy.jsx` and look about 10 lines down. Replace the square character in quotations with the character you copied.

# Limitations
As of this release, the script can't handle:
* Full automation of non-standard card layouts, such as planeswalkers, transforming cards, and Kamigawa flip cards. The script is now capable of proxying planeswalkers, but requires the user to manually position the text as a final step. Transform cards are mostly finished but still a work in progress.
* Quoting something in a card's flavour text without italics. See: Yarok the Desecrated, Phyrexian Altar.
* Snow mana symbols - I haven't gotten around to adding it to the font yet.
