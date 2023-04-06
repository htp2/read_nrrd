Adapted with only minor additions from https://gist.github.com/Nico-Curti/b214c3a715983110ba324ed7c499ac0c

Changes I made: 
1. Added a CMakeLists.txt file to build an executable, which lets OpenCV and Boost be found correctly.
1. Added the 'float' type to the switch statement in the read_nrrd function, so that the program can read float nrrd files. The previous author made this very easy to do thanks to his comments.

Built on Ubuntu 20.04. Tested with both compressed and uncompressed nrrd files and .seg.nrrd files.

# Eventual Use in AMBF
I think we could pretty easily separate out the opencv dependency (we don't need it, it's just used for visualization here). Then we could use this code to read in nrrd files in AMBF. We might need to do a bit more work for parsing the 'color' components of the seg.nrrd files. One nice thing about the (otherwise not so great) PNG load approach was that we could rely on 3D slicer to do the color mapping for us.

TODOs:
- [ ] Settle on a format for 3D (or ND) vectors. Here, it uses ```std::vector<cv::Mat>```, I have used ```std::vector<<std::vector<std::vector<float>>>``` in the past. Others have used some 3DArray struct defined in another codebase. I think we should settle on one and use it everywhere.
- [ ] Make sure we can handle the color mapping in .seg.nrrd files
- [ ] Put this code into AMBF (or a plugin) to read in nrrd files.
- [ ] Adjust the ADF writers (e.g. the slicer plugin) and parser to just point to nrrd files instead of the current .png multiimage format.
- [ ] Convert prior usage of the multiimage format to nrrd files, and consider using nrrd format for other things (e.g., ```voxel_strength```) that are defined in 3D.

# Dependencies
- OpenCV (I tested with 4.2.0)
- Boost (I tested with 1.71.0)

# Build Instructions
```
mkdir build
cd build
cmake ..
make
```

# Usage
```
./read_nrrd <path_to_nrrd_file>
```
