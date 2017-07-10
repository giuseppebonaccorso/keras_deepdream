# Keras-based Deepdream experiment
<img src="https://img.shields.io/github/license/mashape/apistatus.svg?maxAge=2592000"/><br/>

See also: https://github.com/google/deepdream<br/>
Blog entry: https://www.bonaccorso.eu/2017/07/09/keras-based-deepdream-experiment-based-vgg19/<br/>

This experiment (which is a work in progress) is based on some suggestions provided by the Deepdream team in this [blog post](http://googleresearch.blogspot.ch/2015/06/inceptionism-going-deeper-into-neural.html) but works in a slightly different way. I use a Gaussian Pyramid and average the rescaled results of a layer with the next one. A total variation loss could be employed too, but after some experiments, I've preferred to remove it because of its blur effect.

## Requirements
<ul>
<li>Python 2.7-3.5</li>
<li>Keras</li>
<li>Theano/Tensorflow</li>
<li>SciPy</li>
<li>Scikit-Image</li>
</ul>

## Examples
(With different settings in terms of layers and number of iterations)
<table width="100%" align="center">
<tr>
<td width="auto">
<p align="center">
<img src="https://s3-us-west-2.amazonaws.com/keras-deepdream-demo/berlin_dream.jpg" align="center" height="300" width="400">
</p>
<p align="center"><b>Berlin</b></p>
</td>
<td width="auto">
<p align="center">
<img src="https://s3-us-west-2.amazonaws.com/keras-deepdream-demo/berlin_dream_3.jpg" align="center" height="300" width="400">
</p>
<p align="center"><b>Berlin</b></p>
</td>
</tr>
<tr>
<td width="auto">
<p align="center">
<img src="https://s3-us-west-2.amazonaws.com/keras-deepdream-demo/cinque_terre_dream.jpg" align="center" height="300" width="400">
</p>
<p align="center"><b>Cinque Terre</b></p>
</td>
<td width="auto">
<p align="center">
<img src="https://s3-us-west-2.amazonaws.com/keras-deepdream-demo/rome_dream.jpg" align="center" height="300" width="400">
</p>
<p align="center"><b>Rome</b></p>
</td>
</tr>
</table>

## Creating videos
It's possible to create amazing videos by zooming into the same image. You can use the snippet below, which assumes to have already processed an existing image:
```
h, w = processed_image.shape[0:2]

for i in range(500):
    rescaled_image = rescale(processed_image, order=5, scale=(1.1, 1.1))
    rh, rw = rescaled_image.shape[0:2]
    dh = int((rh - h) / 2)
    dw = int((rw - w) / 2)
    zoomed_image = rescaled_image[dh:rh-dh, dw:rw-dw, :]
    processed_image = process_image(preprocess_image(img_as_ubyte(zoomed_image)), iterations=2)
    imsave(final_image + 'img_' + str(i) + '.jpg', processed_image)
```

[This is an animation example](https://www.youtube.com/watch?v=ppUhPBMj-z0)

