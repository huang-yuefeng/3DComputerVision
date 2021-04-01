# source from https://www.youtube.com/watch?v=kyIzMr917Rc
# Stereo (Gilbert Hobrough 1957)
## Invent an analog stereo machine.
# Block World (Larry Roberts 1963)
## Take image of multiple bolcks, extract edges by a grading operator, figure out 3d line configuration, at last render the thing from a new viewpoint.
# Block World ++ (MIT, 1970)
## Vision system recovers the structure of a block scene, robot plans and build an exact copy from another set of blocks.
# Shape from shading (Berthold Horn, 1970)
## infer object shape from one image: if you know one point position in characteristic curve or strip, you can infer other points along it.
# Shape from silhouettes(shading) (Bruce Baumgart, 1974)
## back project image from multiple camera positions: trace a ray from the center of the camera through every point on the silhouette, that give you a conical value which the scene must lie in 3D. From each view you get a different volume which constraints the scene and the intersect of those volumes. This gives approximattion of scene.
# photometric stereo (Bob Woodham, 1977) 
## take multiple images from the same viewpoint under different illuminations, so that is enough hues to reconstruct the object. Moreover, reflectance function is measured so this can be used without the limitation of Lambertian. 
# Essential Matrix (Longuet-Higgins, 1981)
## recover a scene from two projections by a 3\*3 matrix of rank 2. 
# Marching Cubes (Lorensen & Cline, 1987)
## An algorithm to go from a volume to a surface. If you have a volume implicitly representing the surface, you are storing at a voxel in this volume which contains the surface, and they basically tell you how to march in order to stay on surface. Every time you march from one voxel in the surface to another voxel in the surface, you create a polygon according to where the sub-voxel ios-function would intersect that voxel.
# Structure-from-motion by factorization (Tomasi & Kanade, 1990)
## W=MS, W contains the points coordinates of points in image with all X in the first half and all Y in the second half of the matrix, M is the motion of the camera i.e. camera parameters, and S is the shape of the scene i.e. 3D coordinates of real points. It only works for affline projection, so it is not chosen for bundle adjustment 3D reconstruction problems.
# Iterative Closest Points (ICP) (Besl & McKay; Chen & Medion; Zhang, 1992)
## Support you have overlapping range scans of an object, you can use this method to piece them together into a 3D model. The key idea is that use the nearest point as the right correspondence in order to better align the two curves. After multiple iterations, you can get the right correspondence.
# Depth from Defocus (Nayar et al., 1995)
## Take two images with different focus blur cased by different focus setting. Based on the relative blur you can figure out the depth. They found a way that allows you to have two different camera path with two different foucus settings which produce images with the exact same magnification.
# Facade (Devevec, Taylor, Malik, 1996)
## High accuracy 3D modeling based on images which is a predecessor to Google Earth. view-dependent texture mapping.
# Range scan merging (Curless; Hilton, 1996)
## represent the surface is zero, every point in the volume is a distance to that scan. Present every scan as the signed distance function in the volume. Add up all signed distance function and take a level set of that, you can get the optimal surface in the least squred sense.
# Multi-view stereo (Steve Seitz, 1997)
## Voxel Coloring, Space Carving, Level-Set Stereo. Reconstruct 3D model from a set of photos instead of a pair of images.
# Graph cut stereo (Bovcov, Veksler, Zabih, 1998)
## User graph cut as a global optimziation algorithm to find corresponding points in some pair of images.
# Uncalibrated 3D (Pollefeys, Koch, Van Gool, 1998)
## You walk around the scene with video camera and you get out a 3D reconstruction without knowing anything about the camera, such as the parameters or calibrations.
# Morphable Models (Bianz & Vetter, 1999) 
## From a single photo, you can get 3D reconstruction. Not only a single picture information is used, but also a 3D database of 200 scanned people face model is used.A new 3D face is reconstructed by the linear combination of the existing ones in the database.
# Digital Michelangelo Project (Levoy et al. 1999)
## 20 people working for one month scan 2 billion polygons in total 250GB with 1/4 mm precision.
# Camera Tracking (1999)
## A canonical reference on computer based bundle adjustment. Special effect scene is the combination of real footage and CG, and doting that needs to fix the exact position of camera. This needs a lot of bundle adjustment.
# Middlebury Benchmarks (Scharstein et al., 2001) 
## Rigorous evaluation of stereo algorithm. This is a benchmark.
# Helmholtz Stereo (Zickier, Belhumeur, Kriegman, 2002)
## First BRDF-invariant stereo method. For each point, ratio of incident to reflected the light is the same if you swap the camera and the image.
# Laser = Laser Scan (Hernandez & Schmitt)
## No laser can produce 3D geometry that looked as good as a laser scan and arguably is almost as good.
# Photo Tourism (Snavely, Seitz, Szeliski, 2006)
## 3D reconstruction from Internet photos.
# Urbanscape (Nister, Pollefeys, 2006)
## real-time 3D scene capture by driving car around using raw computer vision measurement.
# Aerial 3D (Zebein, Bauer, Karner, Bischof)
## Create 3D model of city from aerial imagery automatically.
# Rome-in-a-day (Agarwal, Snavely, Simon, Sertz, Szelisk, 2009)
## City scale SFM. 
# Kinect (Shotton, et. al. 2011)
## calculate body pose from a single image 200 frames per second.
# From scans to surfaces
## take a few photos and reconstruct a model with the same quality of Lavoy group taking a month.
# Model everything (2015)
## Create a public repository of the world geometry where basically they scan everything, people, places, scenes, things.
# Reconstruct Me (2015)
## Reconstruct yourself including poses expressions and body shapes over time, from your photo collections.
# Inverse CAD (2020)
## CAD models from photographs.
# Visual Turing Test (2020)
## Image-based rendering indistinguishable from reality.
