# Skull-Stripping
Skull stripping is a process of the brain tissue segmentation (cortex and cerebellum) from the surrounding region (skull and non brain area). It is also a very important preprocessing 
step which precedes further analysis in case of many MRI neurological images (such as image registration or tissue classification).

Dataset link : https://brainweb.bic.mni.mcgill.ca/selection_normal.html

Dataset is in the rawb format, raw byte (unsigned) : One (unsigned) byte is used for each voxel, and the data is scaled such that it will use the entire 0...255 range of values. 

RAWB (raw binary) image to a PGM (Portable Gray Map) file Conversion is done.
