Pitch: AI for Controlled Environment Agriculture. From container farms to massive greenhouses, provide the data and model infrastructure for running experiments.

Problem Statement:
* Massive data storage needed for time series data from IoT sensors.
* Sharing of features between plant scientists.
* Easy deployment of new models into experimental framework.
* Tracking of experiments in same building, or between buildings.
* Manage information across different sites (without having to visit locations).
* Detect plant disease and explain conditions that led to it.

Plant Factory:
![alt text](https://github.com/Eochs/AI-System-Designs/blob/main/plant_factory_experiment_tracker.png?raw=true)
1. 


Within the "Sensor Processors" we have Image Processor for segmenting the plant for further processing:
![alt text](https://github.com/Eochs/AI-System-Designs/blob/main/plant_factory.png?raw=true)
1. Training data generation uses a mix of datasets, then perturbs them with GANs (or other method) to see the plant in different configurations, orientations, and lighting. 
  a. Transfer learning from other plant models (similar problem with different leaf shape, etc) can fine tune last layers.
  b. Use 3d model of a plant, simulate same lighting as in the factory, perturbing the leaves and stems to get different arrangements.
  c. etc.
2. We use an off-the-shelf model, such as U-Net, then fine-tune it with our enhanced data set. 
3. We deploy the model to segment live images, to then send to downstream image processing (disease detection and picking decider).

Picking Decider:
Based on visual input, from image segmenter model, and possibly LIDAR for 3D depth information, decide whether we should harvest this plant or not.
1. LSTM for sequence prediction (more water, more of nutrient X, harvest)
2. Simulation errors: have expert gardener that makes decisions at certain points in plant’s life, and see if decision making from model matches.

Order System:
![alt text](https://github.com/Eochs/AI-System-Designs/blob/main/plant_factory_order_system.png?raw=true)
Operator flow:
1. Operator visits a homepage, checks their plants, and requests Application Server for an estimated delivery time.
2. The Application Server sends the requests to the Estimate Delivery Time Service.
3. The Estimate Delivery Time service loads the latest ML model from Model Storage and gets all the feature values from the Feature Store. It then uses the ML model to predict delivery time and return results to the Application Server.

Order System:
1. When plants make progress, i.e., hit certain thresholds of growth or harvesting or packaging the plants, they send the status to Status Service.
2. Status Service updates the order status. 
3. Notification Service subscribes to the message queue and receives the latest order status.
