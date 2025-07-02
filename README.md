
Dataset link : https://brainweb.bic.mni.mcgill.ca/selection_normal.html

# Skull Stripping on Brain MRI Slices

This project implements a basic **skull stripping pipeline** for brain MRI data using Python in Google Colab. The process involves reading a raw binary 3D MRI volume, converting it into 2D slices, applying thresholding, performing row-wise intensity analysis, and generating skull-stripped images.

---

## 📌 Project Workflow:

1. **Mount Google Drive**

Used Google Colab's `drive.mount()` to read/write data from Google Drive.

---

2. **Load Raw MRI Data**

- Loaded a `.rawb` binary volume using NumPy.
- Dimensions: **181 × 217 × 181 (width × height × depth)**.

---

3. **Convert Volume to 2D PGM Slices**

- Saved each MRI slice in `.pgm` format (Portable Gray Map).

---

4. **Region Growing (Initial Experimentation)**

- Performed region growing from a seed pixel.
- Grew regions based on intensity similarity (threshold = 100).
- Saved grown regions as output images.
- ![image](https://github.com/user-attachments/assets/ec9a1cea-b13d-42eb-9b8d-b71f4addecbd)


---

5. **Thresholding**

- Calculated mean pixel intensity for each slice.
- Set pixels below mean to zero (background suppression).
- Saved thresholded slices.
- ![image](https://github.com/user-attachments/assets/306331af-3618-474c-bfdf-87bcbe078095) Thresholded Image on top and original Image on bottom


---

6. **Batch Thresholding (All Slices)**

- Applied the thresholding logic to all 181 slices.
- Output stored in a separate folder.

---

7. **Row-wise Brain Boundary Detection**

- Scanned each row (left-to-right and right-to-left).
- Identified start and end points of bright pixel regions.
- Created a binary mask of detected brain boundaries.

---

8. **Skull Removal Using Boundary Mask**

- Retained pixel values within detected brain boundary.
- Applied morphological operations (opening, closing) to clean binary mask.
- Extracted brain contours and applied them as a mask.
- Final brain-extracted image was generated.
- ![image](https://github.com/user-attachments/assets/a7e5e952-7c13-4dc1-b1e2-39116191aa7d)


---

9. **Row-wise Skull Stripping Algorithm (Full Dataset)**

- For each row in each slice:
  - Scanned left-to-right and right-to-left.
  - Detected intensity transitions with gaps of at least **3 consecutive zero pixels** (used to isolate brain from skull).
  - Set outside skull regions to zero.

- This was done for **all 181 slices**.

---

10. **Visualization**

- Displayed side-by-side plots comparing **original vs skull-stripped images** for slices 50 to 120.
![image](https://github.com/user-attachments/assets/8bf80601-f363-42e3-92dd-204743076792)
![image](https://github.com/user-attachments/assets/c61e6420-9500-4ca3-b9ac-481663e3d503)
![image](https://github.com/user-attachments/assets/2d6e2dec-1abc-4c32-bd19-e1b43f92fa8e)
![image](https://github.com/user-attachments/assets/e12435da-29b5-4b00-8786-ce0c36fa019b)
![image](https://github.com/user-attachments/assets/b3e788aa-6ac8-4984-a5ed-485a10234008)
![image](https://github.com/user-attachments/assets/36b91b4c-1ce6-4662-b449-6d94c0cda08e)
![image](https://github.com/user-attachments/assets/69c57381-eecf-497d-80b2-0593ab36e146)
![image](https://github.com/user-attachments/assets/45906aec-06a4-480a-8f22-7c5d0ecfa863)







---

## 📝 Core Skull Stripping Logic (Pseudocode):

```
For each slice:
    For each row:
        Left-to-right scan:
            - Detect start of positive pixel stream.
            - Detect end after 3 consecutive zeros.
            - Set pixels between start and end to zero.

        Right-to-left scan:
            - Detect end of positive pixel stream.
            - Detect start after 3 consecutive zeros.
            - Set pixels between end and start to zero.

    Save skull-stripped slice.
```

---

## 📂 Output:

- ✅ 181 Original PGM slices  
- ✅ 181 Thresholded slices  
- ✅ 181 Skull-stripped slices  
- ✅ Visualization plots  

---

## ✅ Tools Used:

- Google Colab  
- Python (NumPy, OpenCV, Matplotlib, PIL)  

---
