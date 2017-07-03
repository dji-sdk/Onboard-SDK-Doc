---
title: Camera And Gimbal
date: 2017-03-07
keywords: [single, burst, HDR, AEB, Interval, Timelapse, video resolution, frame rate, aspect ratio, still image, compression, JPEG, DNG, RAW, H.264, MPEG, shutter speed, exposure mode, ISO, Aperture, Exposure Compensation, AE, Auto Exposure, AE Metering, AE Lock, White Balance, Color Temperature, Anti-Flicker, Sharpness, Contrast, Hue, Saturation, Digital Filter, lens, focus, live video feed,  playback manager, media manager, storage, file index, image format]
---

## Introduction

The camera captures photos and videos. Many different modes of operation, resolutions, frame rates, exposure settings, picture settings and file types can be selected. Cameras have local storage to hold the media which will typically be an SD card, and in some cases an SSD (solid state drive). 

This guide covers the large array of settings, modes and functionality provided by DJI cameras. A more general description of camera concepts can be found [here](http://developer.dji.com/mobile-sdk/documentation/introduction/camera_concepts.html).

## Supported Features

Camera and Gimbal modes and features available through DJI Onboard SDK:

* Still and in-motion image capture
* Still and in-motion video capture
* Gimbal angular and velocity rate setters

The camera can only operate in one mode at any one time. For example, media download cannot happen during image capture.

## Image Quality, Resolution and Frame Rate

##### Video Resolution and Frame Rate

DJI Cameras typically support video resolutions of 1280x720 (720p), 1920x1080 (1080p), 2704x1520, 3840x2160 and 4096x2160 (4K). 

Resolution will determine the maximum frame rate able to be captured. The combinations of resolution and frame rate can be queried directly in the SDK, but typically choosing 4K resolution will limit the frame rate to 24/25 fps. Some cameras support up to 120 fps, but only at 1080p resolutions.

##### Still Image Resolution and Aspect Ratio

DJI Cameras have a fixed still image resolution. On some cameras the aspect ratio can be changed between 4:3 and 16:9. Keep in mind that a 16:9 picture is simply a cropped version of a 4:3 image, as the sensor's aspect ratio is 4:3.

##### Compression

All of DJI's cameras support compression for both still images and videos. Some cameras also support uncompressed (RAW) file formats.

The trade-off between capturing RAW and compressed images is:

<table id="t01">
  <thead>
    <tr>
      <th colspan="4">RAW vs Compressed</th>
    </tr>
    <tr>
      <th width=180>Metric</th>
      <th width=100>Raw</th>
      <th width=100>Compressed</th>
      <th>Notes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Image Quality</th>
      <td>Higher</td>
      <td>Lower</td>        
      <td>Compression algorithms are lossy. On small screens this is sometimes not noticeable, but on larger prints, or when capturing scenes with high contrast and color, the difference is more noticeable.</td>
    </tr>
    <tr>
      <td>Post Processing Quality</td>
      <td>Higher</td>        
      <td>Lower</td>
      <td>RAW images use more bits to describe each pixel. This translates to more brightness levels making exposure compensation easier. In a color image where each color is represented by the brightness of a red, green and blue pixel, it also means there are more colors, making white balance adjustments easier.</td>
    </tr>
    <tr>
      <td>Post Processing Necessity</td>
      <td>More Often</td>        
      <td>Less Often</td>
      <td>When exposure and white balance are fine, compressed images will usually require less post processing. If nothing else, to share a RAW image it usually needs to be compressed to a more common file format.</td>
    </tr>
    <tr>
      <td>Compatibility with Media Viewers and Editors</td>
      <td>Fewer</td>        
      <td>More</td>
      <td>Most cameras use different uncompressed image formats making them less likely to be supported by all media viewing and editing programs.</td>
    </tr>
    <tr>
      <td>File Size</td>
      <td>High</td>        
      <td>Low</td>
      <td>Lower file sizes makes storing and sharing media much easier.</td>
    </tr>
    <tr>
      <td>Time Between Shots</td>
      <td>Longer</td>        
      <td>Shorter</td>
      <td>It takes a longer time to process and save a RAW image compared to JPEG. On fixed interval shooting, the difference can be as large as 2s minimum interval for JPEG and 10s for RAW.</td>
    </tr>

  </tbody>
</table>

For still images, DIJ cameras typically support JPEG (compressed) and DNG (RAW) image formats. Cameras can also capture in JPEG + RAW, saving two images for each shot.

For video, only the Zenmuse X5 RAW and X5S supports capturing raw video. RAW video files have a high data rate and large file size and therefore can only be captured onto a solid state drive (SSD). All cameras support compressed formats MP4 (MPEG – 4 AVC) and MOV (H.264).

## Lens and Focus

Most DJI cameras come with a fixed lens, fixed aperture and fixed focus at infinity.

The Zenmuse X5 camera however has a variable aperture, variable focus and the ability to swap lenses between DJI and third party options.

DJI cameras with variable focus allow both manual and automatic focusing. When in automatic mode, the camera will calculate focus from an area in the image, which can be set through the SDK.

Manual focusing is achieved maually setting the focus ring value.

For some lenses, the minimum focus ring value (which corresponds with infinity focus) varies slightly between models and units. Therefore, when using a lens for the first time, a calibration needs to be done:

* Set focus mode to auto
* Point the camera at distant scene
* Ensure the focus target area is pointing at features >30m away
* Let the camera auto focus
* Read the minimum focus ring value

This focus ring value can be tied to the serial number of the camera for future reference.

## Media Storage 

DJI Cameras typically use SD cards to store photos and videos. Depending on whether Class 10 or UHS-1 Micro SD cards of up to 64 GB are required to accommodate the video bandwidths of the various cameras.

The Zenmuse X5 RAW also has a 512 GB solid state drive (SSD) to record video. 4K RAW video data rates can peak at 2.4 Gbps compared to 60 Mbps for MP4 or MOV.

The Inspire 2 (X5S and X4S) uses on aircraft SSD and SD storage instead of on camera storage, while all other cameras use SD cards located on the camera itself, or the gimbal the camera is integrated into.

## General Camera Features

##### Shutter Speed

The time the camera shutter exposes the camera sensor to light is described by the **Shutter Speed**. DJI cameras typically have shutter speeds from 1/8000 s to 8 s. Faster shutter speeds can capture moving features in a scene sharply, but will expose the sensor to less light.

##### ISO

ISO relates to the amount of amplification applied to each pixel. Higher ISO will increase amplification and therefore exposure, but will also increase noise in the picture. Higher ISO is effectively making the camera more sensitive to light, and is useful when trying to capture darker scenes. 

Different DJI cameras have different ISO ranges. The Zenmuse X5 has an ISO range of 100-25600.
  
##### Aperture

The camera aperture controls how large the **window** the sensor can see the world through. Increasing the aperture will increase the amount of light incident on the camera, and therefore increase the exposure. It will also make the depth of field shallower. A shallower depth of field will mean that features at different distances to the camera will be more out of focus. This can create a great effect if trying to highlight the subject (in focus foreground, blurred background), but can be challenging if trying to capture both the foreground and background in focus.

Aperture is measured in f-numbers or f-stops, where the numbers relate to the aperture diameter. A doubling of aperture area, is equivalent to multiplying the diameter by 1.414 (square root of 2), and increases the exposure by one stop.

Cameras on the Phantom and Mavic series of products have fixed aperture lenses (e.g. f/2.8). The Zenmuse X5 has an aperture range of f/1.7 to f/16.

##### Exposure Compensation

In the Program, Aperture Priority and Shutter Priority exposure modes, the exposure compensation value changes the exposure target the camera is using to calculate correct exposure and is set by the user. This can be used to capture darker or lighter images.

In the Manual exposure mode, this value is reported from the camera and reports how much the exposure needs to be compensated for to get to what the camera thinks is the correct exposure. 

##### AE (Auto Exposure) Metering

Exposure is measured by the camera by examining (metering) the pixels in an image. Metering can be set to either the whole image, or just part of the image (the center position or a custom position). This allows scenes that have a high dynamic range of light to be captured with the desired parts having correct exposure.

##### AE (Auto Exposure) Lock

If exposure is being calculated automatically, shutter, aperture and ISO settings might be changing dynamically. AELock allows a freeze of exposure setting changes without needing to change the exposure mode. This can be used to automatically set the exposure of a subject in a scene before moving the camera to frame the subject in a more interesting way (without the exposure changing).

## Not Supported Features 

List of Camera features not supported by DJI Onboard SDK:

* Photo Quality
* Exposure Options
* Shutter Speed
* Picture Settings:
  * White Balance and Color Temperature
  * Anti-Flicker
  * Sharpness
  * Contrast
  * Hue Saturation
  * Digital Filter
* Live Vide Feed
* Broadcast
* Playback Manager
* Media Manager

