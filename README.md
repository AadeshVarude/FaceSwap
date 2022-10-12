# FaceSwap

#Traditional Approach
![image](https://user-images.githubusercontent.com/50541542/195431131-ce3b5c6f-d2e8-4666-b9cb-c5723b816ca9.png)


 #Facial Landmarks detection
 The first step in the traditional approach is to find facial landmarks (important points on the face) so that we have one-to-one correspondence between the facial landmakrs. This is analogous to the detection of corners in the panorama project. One of the major reasons to use facial landmarks instead of using all the points on the face is to reduce computational complexity. Remember that better results can be obtained using all the points (dense flow) or using a meshgrid. For detecting facial landmarks we’ll use dlib library built into OpenCV and python. A sample output of Dlib is shown below.
 ![image](https://user-images.githubusercontent.com/50541542/195431210-a1746047-da10-48ae-9e88-e2f7909a5ba4.png)

#Face Warping using Triangulation
Like we discussed before, we have now obtained facial landmarks, but what do we do with them? We need to ideally warp the faces in 3D, however we don’t have 3D information. Hence can we make some assumption about the 2D image to approximate 3D information of the face. One simple way is to triangulate using the facial landmarks as corners and then make the assumption that in each triangle the content is planar (forms a plane in 3D) and hence the warping between the the triangles in two images is affine. Triangulating or forming a triangular mesh over the 2D image is simple but we want to trinagulate such that it’s fast and has an “efficient” triangulation. One such method is obtained by drawing the dual of the Voronoi diagram, i.e., connecting each two neighboring sites in the Voronoi diagram. This is called the Delaunay Triangulation and can be constructed in O(nlogn) time. We want the triangulation to be consistent with the image boundary such that texture regions won’t fade into the background while warping. Delaunay Triangulation tries the maximize the smallest angle in each triangle.

![image](https://user-images.githubusercontent.com/50541542/195431300-be0af71f-c6d5-4e0e-96cc-98eb8dc0c9c4.png)




