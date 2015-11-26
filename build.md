# How to build and run
# Camera configuration and aruco board creation

1. Go to the cloned ```opencv_contrib``` repo; ```opencv_contrib/modules/aruco/samples```
1. The existing ```CMakeLists.txt``` does not work out of the box for some reason, therefore replace the contents of that file with: 
```
cmake_minimum_required(VERSION 2.8)
project( calibrate_camera_charuco)
find_package( OpenCV REQUIRED )
add_executable( calibrate_camera_charuco calibrate_camera_charuco.cpp )
add_executable( create_board_charuco create_board_charuco.cpp )

target_link_libraries( calibrate_camera_charuco ${OpenCV_LIBS} )
target_link_libraries( create_board_charuco ${OpenCV_LIBS} )
```
3. ```mkdir build && cd build && cmake .. && make```

## Create a charuco board
```./create_board_charuco -o board.png -w 5 -h 10 -sl 50 -ml 30 -d 9 -si```
Then print the created board.png image to a piece of paper.

## Calibrate camera
```./calibrate_camera_charuco -o cameraparams.txt -w 5 -h 10 -sl 50 -ml 30 -d 9```

## Use the new configuration
1. Put the given config file in the ```extra``` dir.
1. Edit ```extra/config.yml``` to use the new camera configuration file.
1. Build the project:
```
mkdir
cd build
cmake ..
make
```
5. Run: ```./detect_markers -conf ../extra/config.yml -ci 0 -L log.txt -r```. Remove ```-r``` to not show all found 'compartments'