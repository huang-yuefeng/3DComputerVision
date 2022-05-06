# Fix AliceVision Installation Issues
	
	
	
----------
* <font size=5>`Fix make test memory error in globalSfM_test`</font>
After `configure` and `make`, there is memory error when running `make test`
1. Fix which line cause this bug by disabling source codes line by line with `//`. Find the error is in second test case
`BOOST_CHECK (sfmEngine.process());` 
of source code`/AliceVision/src/aliceVision/sfm/pipeline/global/globalSfM_test.cpp`.
2. Continue to find the exact point of where error occurs by disabling source codes by `//`. It is boring, if you have more efficient method to find call stack such as gdb, please let me know.
Finally I found the error is in
`dx = H11p.ldlt().solve(w1p);`
of source code `/AliceVision/src/aliceVision/multiview/rotationAveraging/l1.cpp`.
3. Add more test to find the reason. This line source code is to resolve linear equation by `ldlt`, so the matrix `H11p` must has non-zero determinant. Add `std::cout << H11p.determinant() << std::endl;` to test this. This generates the same error as `ldlt()`.
4. The exact reason may be `eigen` related `so` has some issue depending by AliceVison. Update `eigen` installation from version `3.3.7` to `3.4.0`.  Moreover, update `ceres-solver` from version `1.14.0` to `2.1.0`. This memory error disappeared.
5. Reset source code to original version with previous memory error to test. All bugs are clean.
	
```mermaid
			graphLR
			
			
			av-->assimp((Assimp>=5.0.0))
			av-->geogram((Geogram>=1.7.5))
			
			av((AliceVision))-->cmake((CMake=3.16.0))
			av-->cpp
			av-->boost((Boost=1.70.0))
			av-->zlib((Zlib))
			av-->openexr
			av-->opencv(Opencv=4.1.0)
			av-->ceres((Ceres=2.1.0))
			av-->eigen((Eigen=3.4.0))
			av-->oiio((OpenImageIO>=2.1.0))
			
	
			oiio-->cmake
			oiio-->cpp(c++14)
			oiio-->openexr(OpenEXR=3.1.5)
			oiio-->libtiff(libTIFF>=3.9)
			oiio-->libjpeg(libjpeg>=8 or libjpeg-turbo>=1.1)
			oiio-->boost
			oiio-->zlib
			oiio-->opencv
			oiio-->ffmpeg(ffmpeg=3.0)
			oiio-->openvdb(OpenVDB=9.0.0)
			oiio-->tbb
			
			openexr-->imath(Imath=3.1.4)
			
			ceres-->eigen
			opencv-->contrib(contrib=4.1.0)
			openvdb-->tbb(oneTBB=2021.5.0)
			ceres-->suitesparse(with SuiteSparse=4.0)
			suitesparse-->tbb
			ceres-->tbb
	       
```
