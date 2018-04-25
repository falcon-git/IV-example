This is an example of standalone H5P content creted manually. It is the Interactive Video example from H5P.org(https://h5p.org/interactive-video). It is put together very quickly and most (like 99 %) of the library files are unnecessary since the css and js is part of the aggregated files, I just didn't have the time to figure out exactly which ones are needed.

# How to use it?
Put this code on a web server and make sure the url property in js/h5p-integration.js points to the folder where you keep this content

# How was it made
Quick notes:
1. Go to https://h5p.org/interactive-video
2. Create index.html by copying HTML from the H5P iframe on H5P.org/interactive-video
3. Empty div.h5p-content and delete the h5p-initialized class from it. Our scripts are to fill it with HTML.
4. Download all the css and script files referenced by your new index.html and place them in js and css folders
5. Call the aggregated files "aggregated" instead of the hash name they have
6. Change all paths to js and css files, you should have something like this by now in index.html:

```html
<html class="h5p-iframe">

<head>
    <base target="_parent">
    <link rel="stylesheet" href="css/h5p.css">
    <link rel="stylesheet" href="css/h5p-confirmation-dialog.css">
    <link rel="stylesheet" href="css/h5p-core-button.css?p7a34b">
    <link rel="stylesheet" href="css/aggregated.css">
    <script src="js/jquery.js"></script>
    <script src="js/h5p.js"></script>
    <script src="js/h5p-event-dispatcher.js"></script>
    <script src="js/h5p-x-api-event.js"></script>
    <script src="js/h5p-x-api.js"></script>
    <script src="js/h5p-content-type.js"></script>
    <script src="js/h5p-confirmation-dialog.js"></script>
    <script src="js/h5p-action-bar.js"></script>
    <script src="js/aggregated.js"></script>
    <script>H5PIntegration = window.parent.H5PIntegration; var H5P = H5P || {}; H5P.externalEmbed = false;</script>
</head>

<body>
    <div class="h5p-content h5p-frame" data-content-id="618">
    </div>
</body>

</html>
```

7. Replace window.parent.H5PIntegration with the H5PIntegration object in the parent (You can for instance fetch it via the console with JSON.stringify(H5PIntegration) and copy paste it into a new js file called h5p-integration that you include.)
8. Get content files by downloading the .h5p file, rename it to zip, unzip and copy the content folder to your working directory
9. Move all content inside the content folder into a folder called 618 (the content id used on H5P.org)
10. Also get all the other folders from the unzipped h5p files and put them in a "libraries" folder (Lots of files here, you only need very few, typically font files, but we're doing this quickly)
11. change the baseURL and url properties in the beginning og h5p-integration.js to the path to your folder (so that H5P will find all the contents media files)
12. Set postUserStatistics to false in h5p-integration.js (so that H5P doesn't try to store results)
13. Delete any user property in h5p-integration.js (so that H5P doesn't try to resume)
14. Replace all occurences of /sites/default/files/h5p/libraries with ../libraries in css/aggregated.css
