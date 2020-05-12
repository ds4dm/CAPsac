# The Covering-Assignment Problem for Swarm-powered Ad-hoc Clouds (CAPsac): A Distributed 3D Mapping Use-case
Repository containing datasets of the **Covering-Assignment Problem for Swarm-powered Ad-hoc Clouds (CAPsac)** in the context of a swarm-powered 3D mapping mission.

The paper "*The Covering-Assignment Problem for Swarm-powered Ad-hoc Clouds (CAPsac): A Distributed 3D Mapping Use-case*" (preprint available in http://arxiv.org/abs/2004.11837), addresses the problem of optimizing the exploitation of a swarm-powered ad-hoc cloud, by jointly dealing with two interrelated aspects of the data-processing stage:
  - **The workload generation**, i.e., definition of the computing application elements and of the corresponding set of data input.
  - **The workload scheduling/assignment**, i.e., mapping of computing application elements and physical swarm members.

In particular, we consider the generation and placement of workloads whose input data are subject to geolocation/clustering constraints. Practically speaking, the collected data are bound to a location and must be processed in batch of neighboring samples: in the 3D reconstruction use-case, this means that groups of neighboring pictures have to be processed by the same computing element. This additional constraint has a non-negligible impact when dealing with a swarm powered ad-hoc cloud: due to the distributed nature of the swarm-powered data collection stage, the whole input data-set may end up being completely scattered across the UAVs of the swarm. If not properly dealt with during the workload generation/scheduling processes, this aspect may severely deteriorate the whole process performance due to unnecessary data transmission delays (input data must be received by the corresponding computing application element).
 
Briefly, the objective is the minimization of the overall computing times (3D processing stage), including both networking delays caused by the inter-drone data transmission (picture transfers) and computation delays (photogrammetry algorithms).

For the purpose of illustrating the applicability of our approach to a real-life application, we adjust the proposed solution to a relevant use-case scenario from the emergency response field: swarm-powered distributed 3D reconstruction for humanitarian emergency response application. Such use-case is a perfect example of real-life application subject to geolocation constraints and that highly benefits from swarm-powered ad-hoc cloud infrastructure.
  
#### Notation and instances file columns:
 
The names of the instances follow the notation ***"X-ImYYDnZZPWW"***:
  - **X**: *"u"* for the unweighted instances; *"w"* for the weighted instances;
  - **YY**: number of photos; 
  - **ZZ**: number of drones;
  - **WW**: percentage of drones which can do 3D reconstruction(3D-capable). This is always equal to the **floor of (ZZ x WW/100)**; 
  
  
**To solve the problem it is still necessary to define the reliability factor and the maximum transmission time allowed**.


The distinct number of images, drones, and percentage of drones able to perform the 3D mapping are listed as follows.
  - **Images(Im)**: 200, 400, 500, 750, 1000;
  - **Drones(Dn)**: 5, 7, 10, 15, 20, 25; 
  - **Percentage of 3D-capable drones(P)**: 50%, 70%, 90%;
 
Each instance is located into a folder of the name, and they are comprised by tree CSV files: 
  - drones file (*X-ImYYDnZZPWW_drones.csv*);
  - image file (*X-ImYYDnZZPWW_images.csv*); 
  - network topology file (*X-ImYYDnZZPWW_network_arcs.csv*); 

For example, the folder *u-Im200D5P50/*, contains the files *u-Im200Dn5P50_drones.csv*, *u-Im200Dn5P50_images.csv*, and *u-Im200Dn5P50_network_arcs.csv*.

Concerning the columns in the instances files, they are listed as follows.
  - **Drones file**: 
    - **id**: unique ID of a drone
    - **do processing**: *1* if a drone can do 3D resconstruction, *0* otherwise
    - **gps location-alt**: altitude of a drone
    - **gps location-lat**: latitude of a drone
    - **gps location-lng**: longitude of a drone
    - **gps location in 2D-alt**: altitude of a drone when the gps location is projected on a eucledian plane
    - **gps location in 2D-lat**: latitude of a drone when the gps location is projected on a eucledian plane
    - **gps location in 2D-lng**: longitude of a drone when the gps location is projected on a eucledian plane
  
  - **Image file**: 
    - **id**: unique Id of a photo
    - **size(Mb)**: amount of data of the photo in megabytes
    - **processing time(s)**: estimate time to process the photo when performing the 3D reconstruction
    - **photo ownership**: id of drone which had captured the photo
    - **gps location-alt**: altitude of a photo
    - **gps location-lat**: latitude of a photo
    - **gps location-lng**: longitude of a photo
    - **gps location in 2D-alt**: altitude of a photo when the gps location is projected on a eucledian plane;
    - **gps location in 2D-lat**: latitude of a photo when the gps location is projected on a eucledian plane;
    - **gps location in 2D-lng**: longitude of a photo when the gps location is projected on a eucledian plane;
  
  - **Network topology file**: 
    - **id arc ab**: unique ID of an arc
    - **node a**: ID of the source node(drone) *a* in the arc
    - **node b**: ID of the destination node(drone) *b* in the arc
    - **bandwidth**: bandwidth capacity of the arc in megabytes per seconds
