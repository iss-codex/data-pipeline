Accessing CODEX Data
====================

Recommended Level 1 Products
-----------------------------
The Level 1 science data products... 

For most science use cases, the recommended starting point is the Level 2 science data products.


Downloading Data
----------------
Data output from the CODEX data processing pipelines are stored and accessible through the `Solar Data Analysis Center (SDAC) <https://umbra.nascom.nasa.gov/codex>`_. CODEX data products can be downloaded either manually from SDAC, or queried and retrieved using the metadata within individual data products. 

For the latter case, files may be retrieved in one of two ways: 

1. By using the ``wget`` command: 

.. code-block:: bash

wget -r -l1 --no-parent --no-directories -A "codex_level__cl_t1_20251221.fits" -R "*.html*,index*,*tmp*" https://umbra.nascom.nasa.gov/codex/2025/12/21/

In this example, the user would retrieve all  data products from 2025-12-21. To retrieve data from a different date, simply modify the path.

2. By using a data scraping tool. A `Jupyter notebook <https://github.com/nhgodbole/data-pipeline/blob/main/Notebooks/codex_data_scraper.ipynb>`_ was developed for this purpose.

The script queries the database based on user input. By specifying a range of dates, the user can download either Level 1 science data files (if the keyword "calibration" is None) or Level 1 calibration data files (if the keyword "calibration" is not None). Therein, specific calibration types may be specified. 

Reading Data
------------
Standard CODEX data is stored as a standards-compliant FITS file, which bundles the primary data along with secondary data and metadata fully describing the observation.
Each file is named with a convention that uniquely identifies the product. For example, 'codex_level_cl_t1_20251221_000001.fits', where l1 defines the data level,
20251221_000001 is a timestamp in the format yyyymmdd_hhmmss, and _5, _4 are the positions of the filter wheels.

These data are compatible with standard astropy FITS libraries, and can be read in as following the example,

.. code-block:: python

from astropy.io import fits

filename = 'codex_l1_20250521_000001_5_4.fits'

with fits.open(filename) as hdul:
    data = hdul[1].data
    header = hdul[1].header
    uncertainty = hdul[2].data

Data Projections
----------------
The CODEX instrument extends its field of view out to around ??? degrees from the Sun,
creating a meshed virtual observatory extending to a diameter of nearly ??? solar radii.
The wide nature of this field of view requires attention to the data projection being used for these data.

Each data contains a set of World Coordinate System (WCS) parameters that describe the coordinates of the data, in a heliographic (Stonyhurst) coordinate frame.
