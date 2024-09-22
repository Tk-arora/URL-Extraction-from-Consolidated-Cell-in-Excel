![Alt text](https://github.com/Tk-arora/URL-Extraction-from-Consolidated-Cell-in-Excel/blob/main/Screenshot%202024-09-23%20at%203.41.20%20AM.png)
![Alt text](https://github.com/Tk-arora/URL-Extraction-from-Consolidated-Cell-in-Excel/blob/main/Screenshot%202024-09-23%20at%203.49.42%20AM.png)

# README: Extracting URLs from a Consolidated Cell in Excel

## Overview
This guide explains how to extract multiple URLs from a single cell (`B3`) in Excel using a combination of `FIND`, `MID`, and `LEN` functions. The process is visualized in the attached flowchart.

### Formula Used
```excel
=MID($B$3, FIND(C3, $B$3, FIND("http", $B$3, 1)) + LEN($C$3), LEN($C$3))
```

## Step-by-Step Breakdown

1. **Input Cell B3**: Contains multiple URLs.
2. **Step 1: FIND Function**
   - `FIND("http", $B$3, 1)` finds the first occurrence of the text "http" in cell B3.
   - This returns the position of the first URL's starting point.

3. **Step 2: FIND Second Occurrence**
   - `FIND("http", $B$3, 2)` finds the starting position of the second URL in cell B3.
   - The function starts searching from the position after the first occurrence.

4. **Step 3: MID Function**
   - `MID($B$3, start_position, length)` extracts the URL based on the calculated starting position and the length obtained from the first URL.

5. **Step 4: LEN Function**
   - `LEN($C$3)` calculates the length of the first extracted URL to determine where the next URL starts.

6. **Step 5: Next URL Extraction**
   - `FIND(C3, $B$3, FIND("http", $B$3, 1)) + LEN($C$3)` calculates the start position for the next URL extraction, considering the length of the previous URL.

7. **Step 6: Repeat the Process**
   - Dragging the formula down in column C will repeat the extraction process for subsequent URLs.


--- 


## Visual Representation

1. **Extracting the First URL**
   ```
   +------------------------------------------+
   | Consolidated URL in B3                   |
   +------------------------------------------+
   | "http://first-url.com ... http://second" |
   +------------------------------------------+
                       |
                       V
    +--------------------------------+
    | LEFT(B3, FIND("http", B3, 2) - 1) |
    +--------------------------------+
    | Extracted First URL            |
    +--------------------------------+
   ```

2. **Extracting Subsequent URLs**
   ```
   +------------------------------------------+
   | Extracted First URL in C3                |
   +------------------------------------------+
                       |
                       V
    +--------------------------------+
    | MID($B$3, FIND(C3, $B$3, FIND("http", $B$3, 1)) + LEN($C$3), LEN($C$3)) |
    +--------------------------------+
    | Extracted Second URL           |
    +--------------------------------+
   ```

## How to Use

1. Paste the consolidated URLs in cell `B3`.
2. Paste the formula `=LEFT(B3, FIND("http", B3, 2) - 1)` in cell `C3` to get the first URL.
3. Use the main formula `=MID($B$3, FIND(C3, $B$3, FIND("http", $B$3, 1)) + LEN($C$3), LEN($C$3))` in cell `C4`.
4. Drag down the formula to extract the rest of the URLs.

## Conclusion

This method effectively separates multiple URLs stored in a single cell into individual cells, enabling you to manage and analyze them efficiently.

