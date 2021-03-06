# Prepare a Favicon and Other Icons
## Generate Icons

- Prepare the original SVG or PNG icon. PNG should be a 512-pixel square image. Even bigger PNG is recommended to be future proof.
- Upload the original icon to [RealFaviconGenerator](https://realfavicongenerator.net/).
- Configure all the fields.
- Upload `Dedicated picture`s if certain images don't look good.
- Download the package and extract files to a dedicated folder in a project.
- Check the images. If required, replace them with higher quality images. 16x16 and 32x32 icons require a replacement most of the time.
- Images come out uncompressed. It's a good idea to process them with [PNGOUT](http://advsys.net/ken/utils.htm), [SVGO](https://github.com/svg/svgo) or similar tools.
- Recompile `favicon.ico` from 16x16 and 32x32 icons to exclude 48x48 icon. With [ImageMagick](http://www.imagemagick.org/) it could be done with:
        `magick convert favicon-32x32.png favicon-16x16.png favicon.ico`
Note the [order](https://github.com/RealFaviconGenerator/realfavicongenerator/issues/135).

## Webpack

- Configure [copy-webpack-plugin](https://github.com/kevlened/copy-webpack-plugin) to copy all the resources to the output folder.
- Add provided HTML code to the template.

## Backup *(optional)*

Backup should contain:

- Original SVG or 512 pixels or larger square PNG
- Files used to create 16x16, 32x32, or both icons if these icons were overridden
- Files used to create other icons which were overridden
