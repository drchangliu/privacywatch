# The Sensors of Autonomous Vehicles and How They Relate to Data Privacy

## Background

### Autonomous Vehicles

Autonomous vehicles are vehicles that drive themselves, to some extent. They are divided into 6 levels, with level zero being the current level in which the drivers do everything, and level five being the futuristic level in which the car can drive itself as well as a human driver in all situations ([TechRepublic](https://www.techrepublic.com/article/autonomous-driving-levels-0-to-5-understanding-the-differences/)). 

In order for the vehicle to be able to drive by itself, the vehicle needs to be able to see its surroundings. The car uses several sensors that when combined, will theoretically form perfect vision in all situations. In order to accomplish this, the Apollo autonomous vehicles will have different sensors that can work together to gather all the data necessary about the vehicle's surroundings. 

### Privacy Laws

Privacy is a big issue today. In a world surrounded by technology, it's hard to tell who is watching you and who is using your data. In order to protect the general public from having their privacy invaded and their personal information stolen, the government has taken steps to pass laws that can do so. The European Union has created and passed the General Data Protection Regulation (GDPR), which has set requirements that companies must follow regarding the information of their customers. One of those requirements is that the subjects of data processing must specifically consent to it. Another is that the collected data must be anonymized.

While this law only applies directly to the countries in the European Union, it applies indirectly to everyone. Most people use not only the services of companies in their country, but also services of companies in other countries. As citizens protected by the European Union's laws, all services they use must comply with the GDPR. It is hard to specifically block European Union members from a service, so most companies choose to restructure their services so that they comply with the GDPR. 

However, the GDPR is focused specifically on data-collecting services, like Facebook, that collect their user's data and then distribute it to a third party, like advertisers. The GDPR says nothing about autonomous vehicles, which puts the autonomous vehicles in a gray area when it comes to obeying privacy laws.

### Sensor Concerns

One of the sensors used by the Apollo autonomous vehicles is the camera. The cameras used perform the task of any normal cameras, which is take images and videos of its surroundings. However, those images and videos would most likely include people and their faces, should they be passing by during that moment. Taking images with people who have not given their express permission in a setting where their faces are identifiable could potentially be a problem in terms of privacy. If that data is potentially being saved into untracked sources, the problem could be much bigger. Being able to verify if the autonomous system infringes upon future privacy law improvements (as the current laws are aimed at data-collecting services) would be very important.

Would the data collected by autonomous vehicles infringe upon the privacy of individuals?

## Sensors

### Three Main Sensors
These are the three main sensors used by the Apollo autonomous vehicles to sense and interpret their surroundings.

* LiDAR (Light Detection and Ranging)
* Radar (Radio Detection and Ranging) 
* Camera

### Physical Sensor Information

#### LiDAR

LiDAR creates point cloud representations of its surroundings with lasers. The sensor sends the lasers out and waits for laser beams to bounce back to the point of origin. The amount of time the lasers took to bounce back is used to calculate the distance. By using lasers, LiDAR can provide information such as distance and height, a task that would be hard to complete using a flat picture taken by a camera. 

In the point cloud representation, each point represents a laser beam at the point where it has been bounced back. 

LiDAR is best at detecting objects and it functions well in poor lighting. However, it cannot track lanes very well. It is not very good at object classification, its range of visibility is not the best, and excessive small particles caused by bad weather may affect it negatively.

#### Radar

Radar is very similar to LiDAR, but instead of using lasers, it uses radio waves to accomplish its goal. Radio waves have less absorption and can, therefore, work over a longer distance. 

Radar has the largest range of visibility and functions well in poor lighting situations and in bad weather. It can sense objects, but it is not as good at detecting objects as LiDAR is, and it cannot classify objects.

#### Camera

The camera takes images and videos of its surroundings. Those images and videos will then go through multiple stages of processing. The objects in the processed pictures are then classified and the data is used in the decisions the autonomous vehicle makes. For example, the camera feed can be used for lane detection and classifying traffic light colors. 

In some prototype Apollo cars, there are two cameras mounted on the car roof, one with a lens of focal length 25mm, and the other with a lens of focal length 6mm.

Cameras can be limited by poor lighting due to light sources or bad weather. They are not the best at accurately detecting objects, either. Bad weather especially can block their view and hinder them from working properly. 

## Code

### Code Keywords 

#### How many different ways are there to write image or video files to hard disks?

So far, there are three functions and classes that are used in the code to save data (flags, images, video files, etc.) to a destination elsewhere.

* `cv::imwrite()`
* `ofstream`
* `cv::imencode()`

### Code Keyword Information

#### cv::imwrite()

cv::imwrite() is a function that is part of the Open Computer Vision library. It is used to write out images to external sources. In Apollo's code, it is the main function used to write out images.

Its counterpart, cv::imread() is also used in the code.

#### ofstream

ofstream is a very common class that is used by programmers. It is commonly taught in intro classes as the main output stream class that allows programmers to print their output to the screen. In Apollo's code, it is used, among other things, to write out flags, but it has little to do with the images.

#### cv::imencode()

cv::imencode() is a function that encodes an image into a memory buffer by compressing the image and storing it in a memory buffer that is resized to fit the result. 

### About FLAGS

#### FLAGS

Flags are booleans, which are variables that can only be either true or false. In this case, flags are used to control whether the perception module is saving the data or not.

The results of the research conducted over the code state that all places in the code where data could potentially be saved are protected by a flag. The code will not run unless the developer explicitly sets the flag to true, and all debug flags are set to false by default. No PII (personally identifiable information) leaking behaviors in perception module were found during its data processing.

#### GFLAGS

Some flags are defined in gflags (Google's flag library). 

The gflags package contains a C++ library that implements commandline flags processing. It includes built-in support for standard types such as string and the ability to define flags in the source file in which they are used. 

Online documentation available at: https://gflags.github.io/gflags/

### Keyword Search

#### Search of "cv::imwrite()" 
 
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

#### Search of "ofstream"
 
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
