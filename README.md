# Alfred-workflow-photo-keyword-search
A workflow to find keywords in photo .xmp files or embedded in .dng or .cr2 files

This is very much a first release and I am interested to know if it works, and is helpful, for others.

# A note about keywords

Photo keywords may be either flat or hierarchical. By way of example:

`Kolkata, Cat, Home` are "flat" keywords.

`Places|India|Kolkata`, `Animals|Felidae|Domestic cat` and `Places|England|London|Home` are hieracrhical keywords.

You need to set the workflow configuration checkbox to suit the style of keywords that you use. If you do that, and use hierarchical keywords, a search will find anything within the relevant hierarchy (e.g., `India`). If you use hierarchical keywords and _don't_ check the relevant configuration setting your search will find only the last item of the hierarchical keywords (e.g., in this case, `Kolkata`).

As I use hierarchical keywords I've had little chance of testing the workflow against flat keywords so let me know if you experience problems when searching for flat keywords. You may in any event need to experiment with combinations of embedded and heiracrhical keywords in the configuration to discover what provides best results for you.

# Other important notes
1. This version of the workflow will (depending on the settings in the workflow configuration) search for a keyword _only_:
- in sidecar `.xmp` files (the fastest and most efficient search); or
- embedded in either `.dng` or `.cr2` files (a slower search).
2. You can search for more than one word _but only if they are effectively one keyword and the words are separated only by a space_ (e.g., `Botanic gardens`).
3. The search is case insensitive.

# Prerequisites for using this workflow
1. You must have installed the free command line utility [ExifTool](https://exiftool.org/).
2. With version 0.1 of this workflow you must be using either `.cr2` or `.dng` image files—and either:
- be using `.xmp` sidecar files to store the image keywords; or
- be embedding the keywords in the RAW files.

# What this workflow does
The primary purpose of this workflow (designed for photographers) is to allow you to search for a keyword in a photo stored in a selected folder within Alfred's default search scope. As mentioned, the keyword may be stored either in an `.xmp` sidecar file or embedded in either a `.dng` or `.cr2` file (according to the relevant choices in the workflow configuration).
![Start](https://github.com/user-attachments/assets/69a9e917-ea76-4e3d-ba26-ae9c380cb397)

When you have selected the folder and pressed <kbd>⏎</kbd> you will be prompted to give the keyword for which you wish to search:
![Prompt](https://github.com/user-attachments/assets/8a756163-cfc2-4a1d-bbd8-ac922cf5cf28)

Press <kbd>⏎</kbd> and the workflow displays each filename which contains the relevant keyword and you can then search for the filenames as shown (and in this case we're searching for keywords in `.xmp` files):
![Results](https://github.com/user-attachments/assets/1fc2396e-f4e2-4d2b-84d9-8c84f9ec2720)

Note that you can search the results either by the filename or the description.

If, on a selected filename, you press:
- <kbd>⏎</kbd> you can (according to the setting in the workflow configuration) view the related image file either in Alfred's Image View (the default) or in your default app for that file;
- <kbd>⇧</kbd><kbd>⏎</kbd> you can view a selection of the image metadata;
- <kbd>⌥</kbd><kbd>⏎</kbd> you can reveal the related image file in Finder.

*Note that if you view an image in Alfred's Image View or view an image's metadata pressing* <kbd>Esc</kbd> *will take you back to the list of results*.

# Searching for embedded metadata
Searching for metadata embedded in RAW files (see the option in the workflow configuration) is slower than searching for metadata contained in `.xmp` files. I recommend you use it only as a fallback if you have not used sidecar files or if searching the sidecar files does not produce the expected results.


# Why this workflow works as it does
1. It is very much faster to read the initial metadata from `.xmp` files than it is to retrieve metadata which might (or might not) be embedded in the RAW files.
2. The only link between an `.xmp` file and its linked image file (so far as I am aware) is the identical pre-extension name (e.g. `A mountain scene.dng` is linked to `A mountain scene.xmp` simply because both share `A mountain scene` in the filename).
3. As a result of 2 if we scan *all* `.xmp` files in a folder we do not know if they all relate to RAW image files of an identical kind (e.g., all `.dng` files)—or whether there could be mixed among them other files of a different kind (e.g., `.cr2`, `.jpg`, `.tiff`, etc.).
4. When we are dealing with `.xmp` files we have to substitute for the `.xmp` extension the appropriate RAW file extension in order to view the file or extract all of the relevant metadata. That is why the workflow creates a temporary list of all of the relevant files (i.e., those specifically linked to the RAW file extension set in the configuration)—and why you may not see all of the files in a particular folder. In other words, for example, if a folder contains *both* `.dng` and `.cr2` images you will see only those for which you have set the relevant RAW file type in the configuration. You have to run the workflow again, changing the RAW file configuration, to see the other set of RAW files in the folder.

# Adding other RAW file types
It should be possible relatively easily to add other RAW file types to the workflow if there is sufficient interest. In order to do so I would need to know the extension for the RAW file type and also have a sample image file to test.

# A general note
I tend to prefer my [XMP Explorer workflow](https://github.com/Stephen-Lon/Alfred-workflow-xmp-explorer/releases/latest/download/xmp.explorer.alfredworkflow) for finding photos quickly but use this workflow on occasion when looking for a specific keyword. However, in a way (for me, at least) the two workflows are complementary.
