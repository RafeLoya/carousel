# Carousel: A High-Resolution Dataset for Multi-Target Automatic Image Cropping

***Carousel*** is a dataset of 277 images containing multiple subjects. We present it for the pursuit of performing multi-target automatic image cropping to derive multiple crops from a single photograph, with minimal user input.

## Data

Each image contains two or more salient regions and has an average resolution of 10.58 MP. Carousel is organized into two directories with the following structures and file formats:

### `./dataset`

This directory contains the images in their original form. Each photograph has two sidecar files with the naming structure shown below:

```
└─ dataset
   └─ image.jpeg
   └─ image.json
   └─ image_metadata.json
```

`image.json` would contain the label coordinates, along with the image's height and width and other information.

`image_metadata.json` would contain the following information:
- `website_url` - A URL directly to the image.
- `subcrops` - The number of crops that should be derived from the image, which also indicates the number of salient regions.
- `title` - The title of the image as given by where it was sourced from.
- `creator` - Creator of the image.
- `copyright_license_type` - The type of copyright the image falls under.

### `./partitions`

This directory contains the images divided into distinct subregions.

```
└─ partitions
   └─ image
      └─ image_{aspect_ratio}_partition_1.jpg
      └─ ...
      └─ image_{aspect_ratio}_partition_{k}.jpg
      └─ partition_info.json
```

Each image will have partitions according to the value defined in the `subcrops` field in the `_metadata` sidecar file. They will also have a `partition_info.json` file, which records:
- `original_filename`: File name for source image.
- `aspect_ratio_chosen`: Aspect ratio used in the saliency partitioning algorithm, either `3:2` or `2:3`.
- `num_partitions`: A reflection of the `subcrops` field.
- `orientation`: The orientation of the partitions (i.e., `vertical` would be partitioned along the x axis, v.v.).
- `partition_files`: the names of each partition generated for the source image.

### `hard_failures.txt

This file lists images that were not considered successful during the partitioning process. These images usually feature partitions with extreme aspect ratios or that bisect salient regions.

## Sources

Images were sourced from [Wikimedia Commons](https://commons.wikimedia.org/wiki/Main_Page) and image aggregators such as [Flickr](https://www.flickr.com/) and [Rawpixel](https://www.rawpixel.com/). All images were distributed with open, non-commercial licenses.
