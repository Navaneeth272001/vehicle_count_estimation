# vehicle_count_estimation
This repo contains the code the algorithm to predict the number of vehicles required to cover a city for air quality monitoring using low cost devices

## Objective:
- Simulate the trips taken by taxis travelling in Chennai city, assuming the trips are unplanned and ad-hoc.
- Try to predict number of vehicles required to cover a certain percentage of city given the maximum number of vehicles possible.
- Given the road network of a city, come up with approximately optimal number of mobile air quality monitoring device to cover a certain percentage of the city.

## Algorithm
- Create a polygon graph of the city using OSMNX library
- obtain the nodes from the graph and create a dataframe of the nodes
- Initialize Node and Edge Attributes
    - For all nodes:
        - Add visits = 0
        - Initialize popularity with random values
        - Normalize so sum of popularity is 1
    - For all edges:
        - Add visits = 0

- Sample a start node by popularity
- Sample a trip distance "l" from the log-normal distribution
- Find a suitable end node approximately "l" distace away from the current node
- Compute shortest path to the end
- Update:
    - node vists and popularity
    - edge visits
- Popularity of a node increases as the number of visits to that node increases:
    - For each node in the trip path:
        - Increment its visit count by 1
        - Add a small noise (0.01) to the popularity score to avoid 0 probability
        - After updating all relevant nodes, normalize the popularity column
