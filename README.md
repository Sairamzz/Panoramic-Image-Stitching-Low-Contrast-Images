# Panorama Stitching – Low Contrast Images

This project implements a photomosaicing pipeline for low contrast images (Underwater Image dataser), where contrast enhancement and refined homography estimation are necessary for robust stitching. The workflow enhances image quality with CLAHE, extracts SIFT features, matches them using BFMatcher, refines homographies via optimization, and finally stitches all images into a seamless mosaic.

## Acknowledgments

This project was developed as part of coursework under the guidance of Prof. Hanumant Singh, Department of Electrical and Computer Engineering and Program Director of the Master of Science in Robotics program.

The image dataset used for this project was provided by Prof. Hanumant Singh, and is credited to him.

## Functions Overview:

1. ``` normalize_image(img) ```

Converts an image to grayscale and applies CLAHE (Contrast Limited Adaptive Histogram Equalization) for local contrast enhancement. This step improves feature detection in low contrast regions.

2. ``` compute_features(img) ```

Extracts SIFT keypoints and descriptors from the normalized image, returning the keypoints, descriptors, and enhanced grayscale image.

3. ``` match_features(desc1, desc2, ratio=0.8) ```

Matches descriptors between two images using BFMatcher (L2 norm) and Lowe’s ratio test to filter robust feature matches.

4. ``` compute_homography(kp1, kp2, matches, ransac_thresh=3.0) ```

Computes the homography matrix between two sets of matched keypoints using RANSAC to reject outliers. Returns homography, matched points, and the inlier mask.

5. ``` refine_homography(H, pts1, pts2, mask) ```

Refines the homography using Levenberg–Marquardt optimization, minimizing the reprojection error across inlier correspondences for improved alignment accuracy.

6. ``` visualize_matches(img1, img2, kp1, kp2, matches, mask=None, title="", max_draw=100) ```

Displays matches between two images. Optionally filters matches by the inlier mask from RANSAC and visualizes up to max_draw correspondences.

7. ``` draw_matches(imgs, visualize_pairs=None) ```

Runs feature extraction, computes homographies for all image pairs, refines them, and optionally visualizes matches for selected pairs. Returns homographies and match statistics (inlier counts and points).

8. ``` photomosaicing(images, H_Mosaic_List, reference_idx=2) ```

Constructs the final mosaic by chaining sequential homographies to a reference image, warping all input images onto a common canvas, and blending overlaps with weighted averaging. Produces the stitched panorama.

## Results:

### 6 Image Dataset:

<img width="806" height="658" alt="image" src="https://github.com/user-attachments/assets/3d2819d3-ad08-42f8-a6a3-6c136843b1c5" />

### 28 Image Dataset:

<img width="714" height="658" alt="image" src="https://github.com/user-attachments/assets/7a7a19e1-3291-4304-9842-72b75d431bae" />

## How to run:

clone the repo into your local system and run the python notebook (Change the Image destinations in the data folder accordingly)
