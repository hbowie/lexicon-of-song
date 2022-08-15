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
		
## Collection Template File

The Collection template file is named `template.mdtext`, and is generally in the Notenik Note file format. It's a good idea to familiarize yourself with this, as it identifies the field labels and types you have to work with with when sorting and filtering and filling out Merge templates. 

Note that the Collection uses three different classes of Notes: 

- `index` -- The content on the singular Note of this class will become the site's home page. 
- `page` -- These content for Notes of this class will become static pages on the site. 
- `post` -- Notes of this class represent the primary content on the site, and the content that more or less regularly receives new entries. Many of the Collection's fields are primarily applicable to Notes of this class. 

## Script File

When working with a setup like this, I usually find the easiest way to start is to use the **Open Parent Realm** command beneath the **File** menu within Notenik, then select the top-level folder. You will then see a Notenik pseudo-Collection showing all the Collections, script files (and BBEdit project files, if present) found anywhere within. Double click on any of these in order to launch them. When you double-click on a script file, such as the one in this Collection, then Notenik will open the **Scripter** window for you, with the script loaded and ready to run. Just click on the **Go** button to run the script. 

Now let me walk you through the steps in the script, `Generate Website.tcz`, found in the `factory` folder within the `lexicon-content` folder. 

The script file is a tab-delimited file with five columns. The first line of the file contains headings identifying the five columns, and is required. The following lines each specify a Merge template command. Comments identify the steps. 

+ Step 1: Read the content notes for the website. 

	This first step tells the Scripting engine to load the Notenik Collection representing the site's content into memory. Note that the `#PATH#` literal allows you to identify the location of the Collection relative to the location of the script being run. The '`../`' sequence just moves upwards one level in the folder hierarchy. 
	
+ Step 2: Sort posts in descending order by date of post. 

	This step sorts the content into descending order by the `Date of Essay` field, so that the latest posts will appear at the top of subsequent lists. 

+ Step 3: Filter to include only posts. 

	This step filters the Collection so that only Notes with `class` equal to `post` will be considered in the next steps. 
	
+ Step 4: Process merge templates for posts. 

	We have three different templates that require posts as input. The first one formats a file to be placed in the `includes-gen` folder, which will then be included into another template later. The second template just produces one HTML page per post. Note that sort sequence doesn't really matter here, but the filtering criteria are important. And then the third template produces an RSS feed for the site. 

+ Steps 5 - 6: Process Posts in Ascending order. 
		
	The filtering criteria for posts are still in effect, but we have one page where we want to see all posts in ascending order. So we will change the sort, and then process that merge template. 
		
+ Steps 7 - 9: Produce the basic pages. 

	We change the filter criteria here, but we don't worry about sorting, because sequence doesn't make any difference for these pages. 
	
+ Steps 9 - 10: Produce the home page. 

	Since this is only one page, sequence is irrelevant. Note that this is where we include the latest posts from the `includes-gen` folder. 
	
+ Step 11: Generate default CSS. 

	Note that this will only happen when the `styles.css` file does not already exist, so it can be modified as needed later, without fear of it being overwritten. 
	
+ Step 12: Open the just-generated site in the user's Web browser. 

	This assumes you have Apache suitably configured and running on your Mac. 

And there you have it!


