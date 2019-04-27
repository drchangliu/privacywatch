# The Sensors of Autonomous Vehicles and How They Relate to Data Privacy

## Three Main Sensors
These are the three main sensors used by the Apollo autonomous vehicles to sense and interpret their surroundings.

* LiDAR (Light Detection and Ranging)
* Radar (Radio Detection and Ranging) 
* Camera

## Physical Sensor Information

### LiDAR

LiDAR creates point cloud representations of its surroundings with lasers. The sensor sends the lasers out and waits for laser beams to bounce back to the point of origin. The amount of time the lasers took to bounce back is used to calculate the distance. By using lasers, LiDAR can provide information such as distance and height, a task that would be hard to complete using a flat picture taken by a camera. 

In the point cloud representation, each point represents a laser beam at the point where it has been bounced back. 

LiDAR is best at detecting objects and it functions well in poor lighting. However, it cannot track lanes very well. It is not very good at object classification, its range of visibility is not the best, and excessive small particles caused by bad weather may affect it negatively.

### Radar

Radar is very similar to LiDAR, but instead of using lasers, it uses radio waves to accomplish its goal. Radio waves have less absorption and can, therefore, work over a longer distance. 

Radar has the largest range of visibility and functions well in poor lighting situations and in bad weather. It can sense objects, but it is not as good at detecting objects as LiDAR is, and it cannot classify objects.

### Camera

The camera takes images and videos of its surroundings. Those images and videos will then go through multiple stages of processing. The objects in the processed pictures are then classified and the data is used in the decisions the autonomous vehicle makes. For example, the camera feed can be used for lane detection and classifying traffic light colors. 

In some prototype Apollo cars, there are two cameras mounted on the car roof, one with a lens of focal length 25mm, and the other with a lens of focal length 6mm.

Cameras can be limited by poor lighting due to light sources or bad weather. They are not the best at accurately detecting objects, either. Bad weather especially can block their view and hinder them from working properly. 

## Code Keywords 
#### How many different ways are there to write image or video files to hard disks?

These are the functions used in the code to save data (flags, images, video files, etc.) to a destination elsewhere.

* `cv::imwrite()`
* `ofstream`
* `cv::imencode()`


## About FLAGS

### FLAGS

Flags are booleans, which are variables that can only be either true or false. In this case, flags are used to control whether the perception module is saving the data or not.

The results of the research conducted over the code state that all places in the code where data could potentially be saved are protected by a flag. The code will not run unless the developer explicitly sets the flag to true, and all debug flags are set to false by default. No PII (personally identifiable information) leaking behaviors in perception module were found during its data processing.

### GFLAGS

Some flags are defined in gflags (Google's flag library). 

The gflags package contains a C++ library that implements commandline flags processing. It includes built-in support for standard types such as string and the ability to define flags in the source file in which they are used. 

Online documentation available at: https://gflags.github.io/gflags/

## Keyword Search

 ### Search of "cv::imwrite()" 
 
 `cv::imwrite()` (9 usages in 7 files) 
 
 
| File    | Line | Function Name | Usage | Flags Involved |
| ----------- | ----------- |----------- |----------- |----------- |
| [base_map_node.cc](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/localization/msf/local_map/base_map/base_map_node.cc)      | [470](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/localization/msf/local_map/base_map/base_map_node.cc#L470)       | SaveIntenstiyImage(), called from Save(), called from BaseMapNode::Finalize() | Saves/resizes a map image (only if flag is set to be true; false by default).| is_changed_, set to false in Init(), Line 53 |
| [visualization_engine.cc](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/localization/msf/local_tool/local_visualization/engine/visualization_engine.cc)      |[627](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/localization/msf/local_tool/local_visualization/engine/visualization_engine.cc#L627) [664](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/localization/msf/local_tool/local_visualization/engine/visualization_engine.cc#L664)| GenerateMultiResolutionImages() | Copies images. | First usage has no flags and is used upon initialization of the VisualizationEngine. Second usage is controlled by a local variable called "flag" and is true if a path exists. |
| [yolo_camera_detector_test.cc](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/perception/obstacle/camera/detector/yolo_camera_detector/yolo_camera_detector_test.cc) | [133](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/perception/obstacle/camera/detector/yolo_camera_detector/yolo_camera_detector_test.cc#L133)| Test_F | Testing- not part of the final program. | N/A |
| [cc_lane_post_proccessor_test.cc](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/perception/obstacle/camera/lane_post_process/cc_lane_post_processor/cc_lane_post_processor_test.cc) | [77](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/perception/obstacle/camera/lane_post_process/cc_lane_post_processor/cc_lane_post_processor_test.cc#L77) [176](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/perception/obstacle/camera/lane_post_process/cc_lane_post_processor/cc_lane_post_processor_test.cc#L176) | Test_F | Testing- not part of the final program. | N/A |
| [write_img.cc](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/perception/obstacle/lidar/segmentation/cnnseg/write_img.cc) | [58](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/perception/obstacle/lidar/segmentation/cnnseg/write_img.cc#L58)| (int) main() | Saves LiDAR images. | No flags. |
| [tl_preproccessor_subnode.cc](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/perception/traffic_light/onboard/tl_preprocessor_subnode.cc) | [166](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/perception/traffic_light/onboard/tl_preprocessor_subnode.cc#L166)| SubCameraImage() | Saves image (only if flag is set to be true). | FLAGS_output_raw_img is set to false when initialized in [perception_gflags.cc](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/perception/common/perception_gflags.cc#L95), line 95. |
| [tl_proc_subnode.cc](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/perception/traffic_light/onboard/tl_proc_subnode.cc) | [140](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/perception/traffic_light/onboard/tl_proc_subnode.cc#L140) | OutputDebugImg() | Saves image (only if flag is set to be true). | FLAGS_output_debug_img is set to false when initialized in [perception_gflags.cc](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/perception/common/perception_gflags.cc#L96), line 96. |

### Search of "ofstream"
 
 `ofstream` (35 usages in 25 files) 
 
 
| File     | Line | Function Name | Usage | Flags Involved |
| ----------- | ----------- |----------- |----------- |----------- |
| [apollo_app.cc](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/common/apollo_app.cc) | [43](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/common/apollo_app.cc#L43) | ExportFlags() | Exports flags to a file. | No flags. |
| [file.cc](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/common/util/file.cc) | [115](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/common/util/file.cc#L115) | CopyFile() | Copies contents from one file to another. | No flags. |
| [lat_controller.cc](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/control/controller/lat_controller.cc) | [60](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/control/controller/lat_controller.cc#L60) | WriteHeaders() | Writes headers, but only if flag is set to true. | FLAGS_enable_csv_debug is set to false by default. |
| [lat_controller.h](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/control/controller/lat_controller.h) | [203](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/control/controller/lat_controller.h#L203) | class LatController (protected) | Logging purposes for steering. | No flags. |
| [mpc_controller.cc](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/control/controller/mpc_controller.cc) | [59](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/control/controller/mpc_controller.cc#L59) | WriteHeaders() | Nothing. | No flags. |
| [event_collector_main.cc](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/data/tools/event_collector_main.cc) | [82](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/data/tools/event_collector_main.cc#L82) [161](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/data/tools/event_collector_main.cc#L161)| Stop()     SaveEvent() | First usage: Saves event related bags. Second usage: adds new event to a file. | No flags. |
| [hmi_worker.cc](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/dreamview/backend/hmi/hmi_worker.cc) | [109](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/dreamview/backend/hmi/hmi_worker.cc#L109) | SetGlobalFlag() | | |
| []() | []() | | | |
| []() | []() | | | |
| []() | []() | | | |
| []() | []() | | | |
| []() | []() | | | |
| []() | []() | | | |
| []() | []() | | | |
| []() | []() | | | |
| []() | []() | | | |
| []() | []() | | | |
| []() | []() | | | |
| []() | []() | | | |
| []() | []() | | | |
| []() | []() | | | |
| []() | []() | | | |
| []() | []() | | | |
| []() | []() | | | |
| []() | []() | | | |
