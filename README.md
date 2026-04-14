# VO_Tutorial_MindCloud

## What is Visual Odometry ?

visual odometry is using the camera frames and difference between frames to find how much the rover moved in respect with time.

You find the features and landmarks in the image and match them in the next camera frame to estimate how much the camera moved between those two images. Camera Motion can then be tracked to get a stable odometry from a continuous input of images.

This is the CameraInfo message — it describes your camera's properties. Let me explain every field:

header
yamlstamp:
  sec: 0
  nanosec: 0
frame_id: camera_depth

stamp — when this message was sent (0 because Webots sim time)
frame_id — which camera this is (camera_depth)


image size
yamlheight: 480
width: 640

Your camera image is 640 × 480 pixels

distortion_model + d
yamldistortion_model: plumb_bob
d: [0.0, 0.0, 0.0, 0.0, 0.0]

Real cameras have lens distortion (fish-eye effect)
d = distortion coefficients
All zeros = no distortion (perfect simulated camera) ✅


K matrix (most important!)
yamlk:
- 558.89    # fx
- 0.0
- 320.0     # cx
- 0.0
- 558.89    # fy
- 240.0     # cy
- 0.0
- 0.0
- 1.0
This is your 3×3 camera matrix:
K = [558.89,   0.0,  320.0]
    [  0.0,  558.89, 240.0]
    [  0.0,    0.0,    1.0]
ValueMeaningfx = 558.89Focal length in X (pixels) — how much zoom horizontallyfy = 558.89Focal length in Y (pixels) — how much zoom verticallycx = 320.0Image center X = 640/2cy = 240.0Image center Y = 480/2

Used in VO to convert 2D pixel → 3D point:
pythonx = (u - cx) * depth / fx
y = (v - cy) * depth / fy
z = depth

R matrix
yamlr: [1,0,0, 0,1,0, 0,0,1]

Rotation between cameras
Identity matrix = no rotation (single camera) ✅

