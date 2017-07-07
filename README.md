APTK
====

The ASTER Preprocessing Toolkit plugin for ENVI is designed to mitigate multiple issues with how ASTER data are stored, processed, and used by geospatial software packages. It is superior to the processing options available natively in ENVI. The output from an APTK processing run is a new set of ENVI-formatted files, which is consistent with other third party EOS plugins for ENVI (MCTK, EPOC, VCTK, and Hyperion Tools). It currently supports Level 1A, Level 1B, and Level 2 HDF files.

For Level 1A, calibration coefficients are applied to individual bands within a swath (VNIR Nadir, VNIR Backward, SWIR, and TIR), the results are combined into a single cube, and that cube is written out to an ENVI file. That file contains correct band names, wavelengths, and a Rational Polynomial Coefficient (RPC) sensor model to enable orthorectification and, for Band 3N/3B, stereo DEM extraction. It can also correctly align all of the stored bands by taking advantage of available geolocation data and a user-supplied DEM. This does require some interpolation, so you have the option of which method to use.  The end result is a single cube with well-aligned bands, in the original viewing geometry, suitable for analysis and visualization.

Level 1B datasets are notoriously difficult to work with. First and foremost, the scene is projected onto the WGS-84 ellipsoid, which means that the projection was done under the assumption that the Earth is perfectly flat with a height of 0m above the ellipsoid. In mountainous areas, you can see positional errors on the order of 500m when compared to orthorectified Landsat data or Google Earth. Second, the projected scene is rotated such that it mimics the sensor’s orbital scan path, which most geospatial software packages do not like. Third, ENVI is the only software package that offers the option to build RPCs to enable orthorectification and stereo DEM extraction for L1B, but their approach is incomplete and as such requires the user to supply ground control points to bring the data closer to where it is supposed to be on the ground. It in essence reproduces the ellipsoid projection effect unless you force it to consider a different solution via ground control, which puts a significant burden on the user. APTK mitigates all of these issues.

At a minimum, APTK processes each L1B swath in a similar fashion to L1A, producing a calibrated cube with correct band names and wavelengths. Band realignment is not required. Unless you elect to build RPCs, each cube is automatically “unrotated” in its native UTM projection so that North is up, which is what most geospatial software packages prefer. This does require some interpolation, so you have the option of which method to use. If you do elect to build RPCs, swaths are left in their rotated state, but you can then perform orthorectification or, for Band 3N/3B, stereo DEM extraction. The L1B RPCs built by APTK are far more accurate than those built natively by ENVI.

Level 2 datasets are processed in a near-identical fashion to Level 1B, including the application of scale factors to produce scientifically meaningful values and the option to build accurate RPCs.

Please click on the RELEASES button above or follow this link to download the plugin: https://github.com/dawhite/APTK/releases
