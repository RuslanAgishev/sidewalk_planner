# Sidewalk planner
Main road segmentation in street environment for mobile robots.

<img src="https://github.com/RuslanAgishev/sidewalk_planner/blob/master/figures/seg_result.png"/>
<img src="https://github.com/RuslanAgishev/sidewalk_planner/blob/master/figures/seg_result2.png"/>

The main goal of this approach is labeling every pixel on input image which corresponds to a drivable area.
For more information have a look at the [sidewalk segmentation](https://github.com/RuslanAgishev/robot_scene_understanding/tree/master/Sidewalk_segmentation).

Sidewalk local planner [implementation](https://github.com/RuslanAgishev/sidewalk_planner/blob/master/segmented_contour.ipynb)
which produces linear and angular velocity commands based on monocular image input.

<img src="https://github.com/RuslanAgishev/sidewalk_planner/blob/master/figures/APF_planner_example.png"/> <img src="https://github.com/RuslanAgishev/sidewalk_planner/blob/master/figures/middle_planner_example.png"/>

## References
1.  [Small Obstacle Avoidance Based on RGB-D Semantic Segmentation](http://arxiv.org/abs/1908.11675v1)
2.  [Real-time monocular image-based path detection](https://www.researchgate.net/publication/257694570)
3.  [Visual Topological Mapping](https://www.researchgate.net/publication/221229890_Visual_Topological_Mapping)

Building routes on walkable and drivable areas with the help of [OSMNX](https://github.com/gboeing/osmnx)
library [example](https://github.com/RuslanAgishev/sidewalk_planner/blob/master/osmnx_tutorial.ipynb).

<img src="https://github.com/RuslanAgishev/sidewalk_planner/blob/master/figures/osmnx_route_exmaple.png"/>
