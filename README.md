# Lexicon of Song

This repo contains the text files used to create the website at [LexiconOfSong.org](https://lexiconofsong.org).

The website is generated using the [Notenik app](https://notenik.app). 

## Folder Structure

All of the actual HTML files for the site are stored at the top level, along with this `README.md` file, the `LICENSE.md` file and the `rss.xml` file. 

And then there are the following folders.

+ `css` &mdash; This contains the CSS stylesheet used for the site. 
+ `images` &mdash; This contains the image files referenced from the HTML files. 
+ `js` &mdash; This contains whatever javascript is used by the site. 
+ `lexicon-content` &mdash; This contains all of the files used by Notenik to generate the HTML files. This folder can be opened as a Notenik Collection. The files with extension `.mdtext` include the Collection template file (`template.mdtext`) plus all of the actual content (aka "Notes") containing content formatted using Markdown, along with accompanying metadata. Then there are the following subfolders. 
	- `files` &mdash; This contains files attached to the Notes, which are generally image files (that will eventually be copied to the `images` folder described above). 
	- `factory` &mdash; This contains files used by Notenik to transform the content into the actual HTML pages. The sole file found at this level is a Notenik script file (`Generate Website.tcz`) that specifies the sequence of operations to be followed whenever the site is to be regenerated. Then there are the following subfolders. 
		+ `includes-gen` &mdash; This folder is used to store HTML fragments that are created early in the script operations, and then later included into full HTML pages. 
		+ `includes` &mdash; These are static bits of HTML that are included into HTML pages where appropriate. 
		+ `templates` &mdash; These are the Notenik Merge Templates used to format and position the content appropriately in order to generate the final HTML pages. 

		
