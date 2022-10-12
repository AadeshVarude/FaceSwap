# FaceSwap

# Traditional Approach
![image](https://user-images.githubusercontent.com/50541542/195431131-ce3b5c6f-d2e8-4666-b9cb-c5723b816ca9.png)


 # Facial Landmarks detection
 The first step in the traditional approach is to find facial landmarks (important points on the face) so that we have one-to-one correspondence between the facial landmakrs. This is analogous to the detection of corners in the panorama project. One of the major reasons to use facial landmarks instead of using all the points on the face is to reduce computational complexity. Remember that better results can be obtained using all the points (dense flow) or using a meshgrid. For detecting facial landmarks we’ll use dlib library built into OpenCV and python. A sample output of Dlib is shown below.
 ![image](https://user-images.githubusercontent.com/50541542/195431210-a1746047-da10-48ae-9e88-e2f7909a5ba4.png)

# Face Warping using Triangulation
Like we discussed before, we have now obtained facial landmarks, but what do we do with them? We need to ideally warp the faces in 3D, however we don’t have 3D information. Hence can we make some assumption about the 2D image to approximate 3D information of the face. One simple way is to triangulate using the facial landmarks as corners and then make the assumption that in each triangle the content is planar (forms a plane in 3D) and hence the warping between the the triangles in two images is affine. Triangulating or forming a triangular mesh over the 2D image is simple but we want to trinagulate such that it’s fast and has an “efficient” triangulation. One such method is obtained by drawing the dual of the Voronoi diagram, i.e., connecting each two neighboring sites in the Voronoi diagram. This is called the Delaunay Triangulation and can be constructed in O(nlogn) time. We want the triangulation to be consistent with the image boundary such that texture regions won’t fade into the background while warping. Delaunay Triangulation tries the maximize the smallest angle in each triangle.

![image](https://user-images.githubusercontent.com/50541542/195431300-be0af71f-c6d5-4e0e-96cc-98eb8dc0c9c4.png)



Since, Delaunay Triangulation tries the maximize the smallest angle in each triangle, we will obtain the same triangulation in both the images, i.e., cat and baby’s face. Hence, if we have correspondences between the facial landmarks we also have correspondences between the triangles (this is awesome! and makes life simple). Because we are using dlib to obtain the facial landmarks (or click points manually if you want to warp a cat to a kid), we have correspondences between facial landmarks and hence correspondences between the triangles, i.e., we have the same mesh in both images. Use the getTriangleList() function in cv2.Subdiv2D class of OpenCV to implement Delaunay Triangulation. Refer to this tutorial for an easy start. Now, we need to warp the destination face to the source face (we are using inverse warping so that we don’t have any holes in the image, read up why inverse warping is better than forward warping) or to a mean face (obtained by averaging the triangulations (corners of triangles) of two faces). Implement the following steps to warp one face (A or source) to another (B or destination).





# Replace Face

This part is very simple, you have to take all the pixels from face A, warp them to fit face B and replace the pixels. Note that simply replacing pixels will not look natural as the lighing and edges look different. A sample output of face replacement is shown below.

![image](https://user-images.githubusercontent.com/50541542/195433683-a9de5492-41ad-45d5-acb3-3b92d17f6cfd.png)





