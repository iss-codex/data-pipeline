CODEX data structure
====================

Concept
-------
CODEX data is structured using the FITS extension framework. Each file consists of 1 primary header data array, which contains the metadata for the file, 4 secondary data arrays, one for each polarization, along with a corresponding World Coordinate System (WCS) describing the spatial coordinates of the data itself. Another primary data array contains the parameter uncertainties. This allows for better integration with AstroPy software libraries, including coordinate and data reprojection or resampling.
For primary Level 2 CODEX data, connecting data with coordinates is critical given that the instrument is only 2
axis stabilized (azimuth and elevation), so the scene will have an apprent rotation throughout each orbit, aand data analysis is epxected to require both spatial and temporal averaging.
