# WIP

This project is a *work in progress*. The implementation is *incomplete* and subject to change. The documentation can be inaccurate.

# Brief

Examples of Neural-Style on Renaissance paintings on styles based on Impressionism and Photographs.

Neural-Style is an algorithm to generate artistic paintings using Deep VGG Convolutional Neural Networks. The algorithm is exposed here:

     A Neural Algorithm of Artistic Style
        Authors: Leon A. Gatys, Alexander S. Ecker, Matthias Bethge
        At: https://arxiv.org/abs/1508.06576
        August-September 2015

Justin Johnson has an implementation of the Neural-Style algorithm in Torch, available at one of his GitHub repositories: [https://github.com/jcjohnson/neural-style](https://github.com/jcjohnson/neural-style).

The current repository applies that version of Neural-Style on Torch on Renaissance paintings (Leonardo da Vinci's and Sandro Botticelli's) using style images based on Impressionism (Claude Monet's) and normal photographs.

To install the program, consult Justin Johnson's instructions at [https://github.com/jcjohnson/neural-style#setup](https://github.com/jcjohnson/neural-style#setup).

The options to the program are explained in [https://github.com/jcjohnson/neural-style#usage](https://github.com/jcjohnson/neural-style#usage). Here it is used `-gpu -1` to use only the main CPU. To note, this program offers the option to apply a weighted sequence of several style images on the input content image, which is a very powerful resource: the list of style images needs to be separated by "," (commas), without space between the paths to the style-images:

       -style_image  style_image1,style_image2[,...]

Similarly, the optional parameter `-style_blend_weights` is the list of the relative weights each of the style-images will have among them:

       -style_blend_weights  float_weight_style_img1,float_weight_style_img2[,...]

(The number of weights in `-style_blend_weights`, if given, must be the same as the number of style images in `-style_image`.)

Other options to note at first sight are `-save_iter <#-iters>`, to save the transformed image after `<#-iters>` iterations (default: 100) with a filename and format deduced from the `-output_image` filename; and the option `-image_size <#-max-img-dimension-in-pixels>` with the maximum (lateral) dimension the resulting image(s) will have (default is 512, ie., 512 pixels lateral size of the resulting image(s)).

# Examples on some Renaissance paintings:

* Da Vinci's Mona Lisa as content-image with Monet's "Poppy Field near Giverny" as style image (it is noticed here the effects of the lights of Impressionism on that Renassaince painting):

       th neural_style.lua -style_image background_Claude_Monet_Poppy_Field_near_Giverny.jpg \
                           -content_image Da_Vinci_Mona_Lisa.jpg \
                           -output_image Mix_Da_Vinci_Mona_Lisa_Monet_Landscape.png \
                           -gpu -1

<p align="center">
<img src="https://raw.githubusercontent.com/je-nunez/examples_neural-style/master/examples/Mix_Da_Vinci_Mona_Lisa_Monet_Landscape/Da_Vinci_Mona_Lisa.jpg" height="250px">
<img src="https://raw.githubusercontent.com/je-nunez/examples_neural-style/master/examples/Mix_Da_Vinci_Mona_Lisa_Monet_Landscape/background_Claude_Monet_Poppy_Field_near_Giverny.jpg" height="250px">
</p>

Result:

<p align="center">
<img src="https://raw.githubusercontent.com/je-nunez/examples_neural-style/master/examples/Mix_Da_Vinci_Mona_Lisa_Monet_Landscape/Mix_Da_Vinci_Mona_Lisa_Monet_Landscape.png" height="500px">
</p>


* Boticelli's Primavera as content-image with a real-life photograph of the Avenue of Live Oaks at Boone Hall in Mount Pleasant, South Carolina (planted in 1743) as style image:

       th neural_style.lua -style_image background_Claude_Monet_Poppy_Field_near_Giverny.jpg \
                           -content_image Da_Vinci_Mona_Lisa.jpg \
                           -output_image Mix_Da_Vinci_Mona_Lisa_Monet_Landscape.png \
                           -gpu -1

<p align="center">
<img src="https://raw.githubusercontent.com/je-nunez/examples_neural-style/master/examples/Mix_Boticelli_Avenue_Oaks_Boone_Hall/Boticelli_Primavera.jpg" height="250px">
<img src="https://raw.githubusercontent.com/je-nunez/examples_neural-style/master/examples/Mix_Boticelli_Avenue_Oaks_Boone_Hall/background_Avenue_Oaks_Boone_Hall_Mount_Pleasant_South_Carolina.jpg" height="250px">
</p>

Result:

<p align="center">
<img src="https://raw.githubusercontent.com/je-nunez/examples_neural-style/master/examples/Mix_Boticelli_Avenue_Oaks_Boone_Hall/Mix_Boticelli_Avenue_Oaks_Boone_Hall.png" height="500px">
</p>


* Boticelli's Primavera as content-image with Monet's "Spring in Giverny" (1890) as style image:

       th neural_style.lua -style_image background_Claude_Monet_Spring_in_Giverny_1890.jpg \
                           -content_image Boticelli_Primavera.jpg \
                           -output_image Mix_Boticelli_Claude_Monet_Spring_in_Giverny_1890.png \
                           -gpu -1

<p align="center">
<img src="https://raw.githubusercontent.com/je-nunez/examples_neural-style/master/examples/Mix_Boticelli_Claude_Monet_Spring_in_Giverny_1890/Boticelli_Primavera.jpg" height="250px">
<img src="https://raw.githubusercontent.com/je-nunez/examples_neural-style/master/examples/Mix_Boticelli_Claude_Monet_Spring_in_Giverny_1890/background_Claude_Monet_Spring_in_Giverny_1890.jpg" height="250px">
</p>

Result:

<p align="center">
<img src="https://raw.githubusercontent.com/je-nunez/examples_neural-style/master/examples/Mix_Boticelli_Claude_Monet_Spring_in_Giverny_1890/Mix_Boticelli_Claude_Monet_Spring_in_Giverny_1890.png" height="500px">
</p>


* As an example of applying a weighted sequence of style images to an input content image, it appears below Boticelli's Primavera as content image, and style-images the weighted sequence of a photography of Algonquin Provincial Park, the Avenue of Live Oaks at Boone Hall (S.C.), and the Monet's painting "Spring in Giverny" (1890), in that order, with relative weights 10, 10 and 15 among the three, respectively:

       th neural_style.lua \
            -style_image Autumn_in_Algonquin_Park.jpg,background_Boone_Hall_Mt_Pleasant_South_Carolina.jpg,background_Claude_Monet_Spring_in_Giverny_1890.jpg \
            -style_blend_weights 10,10,15 \
            -content_image Boticelli_Primavera.jpg \
            -output_image Mix_Boticelli_Algonquin_Park_Boone_Hall_SC_Monet_Spring_in_Giverny.png \
            -gpu -1

<p align="center">
<img src="https://raw.githubusercontent.com/je-nunez/examples_neural-style/master/examples/Mix_Boticelli_Algonquin_Park_Boone_Hall_SC_Monet_Spring_in_Giverny/Boticelli_Primavera.jpg" height="250px">
<img src="https://raw.githubusercontent.com/je-nunez/examples_neural-style/master/examples/Mix_Boticelli_Algonquin_Park_Boone_Hall_SC_Monet_Spring_in_Giverny/Autumn_in_Algonquin_Park.jpg" height="250px">
<img src="https://raw.githubusercontent.com/je-nunez/examples_neural-style/master/examples/Mix_Boticelli_Algonquin_Park_Boone_Hall_SC_Monet_Spring_in_Giverny/background_Boone_Hall_Mt_Pleasant_South_Carolina.jpg" height="250px">
<img src="https://raw.githubusercontent.com/je-nunez/examples_neural-style/master/examples/Mix_Boticelli_Algonquin_Park_Boone_Hall_SC_Monet_Spring_in_Giverny/background_Claude_Monet_Spring_in_Giverny_1890.jpg" height="250px">
</p>

Result:

<p align="center">
<img src="https://raw.githubusercontent.com/je-nunez/examples_neural-style/master/examples/Mix_Boticelli_Algonquin_Park_Boone_Hall_SC_Monet_Spring_in_Giverny/Mix_Boticelli_Algonquin_Park_Boone_Hall_SC_Monet_Spring_in_Giverny.png" height="500px">
</p>

