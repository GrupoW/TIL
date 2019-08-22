## Batch resizing images from the command line on a Mac

If you need to quickly resize a bunch of images on a Mac, you don't need to open Photoshop. There's a simple way to do it from the command line, by using the sips command. This is the basic syntax:

```
sips -Z MAX_SIZE FILE_NAME
```

### Resizing single images

By way of example, to resize a single image to a maximum of 800px (either width or height), you'd use the following. It's important to note that this will replace the existing image, so make a copy you want to keep the original.

```
sips -Z 800 image.jpg
```

### Batch resizing images

Where sips really comes into it's own however is for folders of images. To resize multiple images just use a wildcard (*) selector together with the file extension (.jpg in this case). The example below will blast through all the images in folderName, resizing them to 1200px in a flash.

```
sips -Z 1200 folderName/*.jpg
```

@reference: [Batch resizing images from the command line on a Mac](https://jameschambers.co/writing/batch-resize-images-mac-command-line/)

