#  Semi-automated object extraction from large-scale historical maps

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.6906425.svg)](https://doi.org/10.5281/zenodo.6906425)

**Author**: Inga Schlegel

**Date**: 12/17/2022

Exemplary research data and software used and implemented for the KN paper *Semi-automated object extraction from large-scale historical maps* [TO DO add paper link].

This repository contains executable Python code (Jupyter Notebooks) described within sections 4 and 5 in the paper. Each subfolder *data* contains exemplary input data.

All \*.ipynb files can be executed directly within Jupyter Notebook. To install and set up Jupyter Notebook via `conda` or `pip` see [Jupyter's installation guide](https://jupyter.org/install).


## Library requirements

The Python libraries needed for the \*.ipynb files are listed within *requirements.txt*. They can be installed with `pip install -r requirements.txt`.


## 01 Elimination of labels

The following example gives detail of the Jupyter Notebook's proceeding with the aim to eliminate text but no building edge from the input map (see paper section 4.1).

1. With the help of Python’s library *OpenCV*, the considered text image area was converted into grayscale.

    ![](https://github.com/IngaSchl/Object-Extraction/blob/main/figures/1.png)

2. A binary mask was generated based on the grayscale image and a threshold (here: 150) to separate dark ‘foreground’ from bright ‘background’ pixels.

    ![](https://github.com/IngaSchl/Object-Extraction/blob/main/figures/2.png)

3. All conditions, which had to be met in order to reclassify a former “foreground” pixel of the binary mask into a “building edge” pixel of the 3-class mask, are described below. All remaining “foreground” pixels were classified as “text” pixels. Not all conditions are met within the shown example but apply for others.

    3.1. Only the upper five and lower five rows were considered (with)in this step as building edges usually only appear in this area of the text image area. This threshold (here: 5) had to be adjusted for few cases.
  
    (a) Pixel is within a row consisting of 100% “foreground” pixels.
    
    (b) Pixel is within a row with more than 30% “foreground” pixels **and** with more than 40 “foreground” pixels side by side. These thresholds (here: 30% and 40) had to be adjusted for few cases.
    
    (c) Pixel in the **upper** image part is within a row **above** another row which was already classified as “building edge” in (a) or (b).
    
    (d) Pixel in the **lower** image part is within a row below another row which was already classified as “building edge” in (a) or (b).

    ![](https://github.com/IngaSchl/Object-Extraction/blob/main/figures/3-1.png)

    3.2. Considering only the very first and very last rows: Pixel is within a row with 15 “foreground” pixels side by side. This condition is not met by the shown example but applies for others.

    ![](https://github.com/IngaSchl/Object-Extraction/blob/main/figures/3-2.png)

    3.3. Considering only the upper four and lower four rows.
    
    (a) Pixel is within a row which already contains “building edge” pixels from 3.1. or 3.2.
    
    (b)	Pixel in the **upper** image part is within a row not containing ‘building edge’ pixels and **above** another row which already contains “building edge” pixels from 3.1. or 3.2.

    (c)	Pixel in the **lower** image part is within a row not containing ‘building edge’ pixels and **below** another row which already contains “building edge” pixels from (3.1) or (3.2).
    
    ![](https://github.com/IngaSchl/Object-Extraction/blob/main/figures/3-3.png)
    
4. A new binary mask – consisting of the two classes “text” and “background” – could be generated by excluding the class “building edge”.

    ![](https://github.com/IngaSchl/Object-Extraction/blob/main/figures/4.png)


## 02 Object extraction

Detailed object extraction process trees – described in general terms in paper sections 4.2 and 6 (for the maps shown in figures 1 as well as 8 a) and b), respectively) - are provided in the form of .txt files. These process trees can be implemented directly in eCognition.
