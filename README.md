# azgaar-to-foundry-workflow
instructions and notes for importing azgaar data into foundry

# instructions for importing The Roil's Azgaar's map data into Foundry hosted on The Forge

## dependencies
- [https://azgaar.github.io/Fantasy-Map-Generator/](https://azgaar.github.io/Fantasy-Map-Generator/)
	- access this online at the above url or gitclone your own local copy of the software.
	- if you comfortable with git, it is recommended to do this since large maps can require significant memory so a local copy is much easier to work with than via the website
- [https://www.gimp.org/](https://www.gimp.org/)
	- for image manipulation
- a license for [https://foundryvtt.com/](https://foundryvtt.com/)
- an active subscription for [https://forge-vtt.com/](https://forge-vtt.com/)
	- Foundryvtt may be hosted by other means. These instructions are for my setup where I host foundryvtt on The Forge.
- foundry module: [Unofficial Azgaar's fantasy Map Generator Import](https://github.com/Ethck/azgaar-foundry)

## open Azgaar .map file
1. open the Azgaar app or navigate to the website.
2. click the "Load" button in the expandable side menu.
3. load the `.map` file from machine (if loading from local) or whatever other location you have stored your `.map` at. I typically store my `.map` files on google drive and download them locally when needed for use.

## export Azgaar .png
This .png will eventually be used as the background map image in the foundry scene.
Whatever is visible here, will be visible there so choose your currently active/visible layers appropriately.

### which layers to show
My preference is to display mainly physical layers:
1. Biomes
2. Grid
3. Rivers
4. Routes
5. Rulers
6. Scale Bar

### to export
1. make the window fullscreen (default is `f11` key)
2. click the export button
3. Under the "Download imag" heading, set the "PNG/JPEG scale" to 2. This is important for grid scaling once imported into Foundryvtt.
4. click the .png button. This will write a lossless compressed .png file to your Downloads dir (by default on windows). This file will be named according to the date following this convention: "[mapname] YYYY-mm-dd-HH-MM-SS.png". For example: `Zendikar 2022-11-14-16-52.png`.
5. Close Azgaar's app

## convert .png to .webp
This is an optional but recommended step since foundryvtt is optimized for .webp files.
1. open the `Zendikar 2022-11-14-16-52.png` file in GIMP.
2. `File -> Export As...` will spawn a popup window
3. In the "Export Image" popup window, change the .png in the `Name:` field to `.webp`.
4. Click the "Export" button which will spawn a popup window.
5. In the "Export Image as WebP" popup window,
	1. check "Lossless"
	2. "Source type" should be set to "Default"
	3. uncheck "Save Exif data"
	4. uncheck "Save IPTC"
	5. uncheck "Save XMP data"
	6. check "Save color profile"
	7. uncheck "Save thumbnail"
	8. click "Export" button
	9. wait a few moments, the "Export Image" window will disappear once the `.webp` file has finished writing.
6. close GIMP app

## upload .webp to Forge (cloud) storage
This will be the final location for the .webp file for the scene to reference. Moving the file afterward will break the link in the Foundry Scene data and would need to be redefined at that time; choose your location carefully to avoid any link breaking issues in the future.
That said, any location on the Forge's (cloud) storage will work.
1. log into your Forge account using Firefox (preferred) or Chrome (fallback to this if issues with Firefox).
2. click on the "Asset Library" button at the top of the webpage
3. navigate to the desired location to upload the `.webp` file to. For example, `Assets Library/The Roil/azgaar`
4. click the "Upload Assets" button. In the popup window, select the `.webp` file.

## import into foundry using the "Unofficial Azgaar's fantasy Map Generator Import" module
1. go to the settings tab in the Foundryvtt world where you wish to import the map
2. click the "Configure Settings" button.
3. In the popup window "configure Game Settings", enter "azgaar" into the "Filter" field.
4. Scroll down in the right pane of the popup window until you get to the Azgaar section, all other sections should be collapsed due to the "azgaar" term in the "Filter" field.
5. Click the "Load Azgaar's Map into Foundry".
6. In the popup window "Load Azgaar's Map",
	1. click the "Browse..." button and "Open" your local `.map` file.
	2. click the "Link to Picture" button, and navigate to your `.webp` file. Once chosen, the path to that file should be seen in the field above "Link to Picture".
	3. under the "MapNote Icon Select", check "Use FMG Colors?" for the following (this is largely preferential):
		- Burgs
		- Countries
		- Provinces
	4. click the "Import" button.
7. a series of blue banners will appear as the data is imported and compendia are created. The process is complete when the popup window "Load Azgaar's Map" closes automatically.
8. close the "Settings" window.

## The Azgaar map scene
The scene should now have a lot of journal notes on it at first with the scene title being the filpath to the `.webp`.

### fix the scene name
1. right click the scene button at in the scene navigation area (at the top of the window by default).
2. in the dropdown, click 'Configure'
3. in the popup "Configure Scene: [path to `.webp`]", change the "Scene Name" field to your liking. For example, "Zendikar Map".
4. Set Permissions to
	1. check "Show in Navigation"
	2. click the drop down to the right of this checkbox to "All Players" so that all players can navigate to this scene.
5. click the "Save Changes" button

After zooming, they should reset and most will go invisible, and reappear at certain zoom levels.
These journal notes however or usually offset as is the foundry grid.
To fix this:
1. right click the scene button at in the scene navigation area (at the top of the window by default).
2. in the dropdown, click 'Configure'
3. in the popup "Configure Scene, click the "Grid" tab.
4. in the new tab, click the right-angled ruler button next to the "Grid Type" field
5. in the popup "Grid Configuration Tool", set
	1. "Grid Type" to "Hexagonl Rows - Odd"
	2. "Background image Scale" to 1
	3. "Grid Size" to 50
	4. click the "Save Changes" button
	5. in the popup, click "yes"
6. Now the grid is almost correct but still a little finnicking to do...open up the "Grid Configuration Tool" popup again.
	1. Use the down arrow key to slide the grid until the hex lines match up. This will lead to a change in the "Background Image Offset" "y" value. For example, y = -84.
	2. click the "Save Changes" button.
7. Now the Foundry grid and the Azgaar's `.webp` grid should be directly overlapping. Additionally, the journal notes are placed appropriately where, previously, they were also offset slightly.
8. click the "Save Changes" button in the "Confugure Scene: [map name] Map" (e.g. "Configure Scene: Zendikar Map").

### journal note location
The importer imports the journal notes into compendia to avoid performance issues with so many journal notes.
These compendia are loaded into the "Defaults" section of the Compendia tab automatically. To find them,
1. click the "Compendium Packs" tab
2. click the "Default" category
3. The Azgaar compendia are in the following folders:
	- Religions
	- Cultures
	- Provinces
	- Countries

Each journal note pinned to the scene opens a journal from one of these compendia.

## That's it, happy worldbuilding!