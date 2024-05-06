# Running From The Night: Calculating The Lunar Magellan Route in Parallel

## Authors: Kevin Fang and Nikolai Stefanov

### URL: [thesnakefang.github.io](https://thesnakefang.github.io)

### Documents

- [Project Proposal](proposal.pdf) (PDF)
- [Milestone Report](milestone.pdf) (PDF)
- [Final Report](finalreport.pdf) (PDF)

---

#### Contact

- Kevin Fang - [kevinfang@cmu.edu](mailto:kevinfang@cmu.edu)
- Nikolai Stefanov - [nstefano@andrew.cmu.edu](mailto:nstefano@andrew.cmu.edu)

#### Repository

- [GitHub Repository](https://github.com/TheSnakeFang/thesnakefang.github.io)

#### About

Parallel application using MPI in C++ to calculate the shortest safe path between two locations on the moon on-the-fly using Lunar Reconnaissance Orbiter (LRO) lunar surface imagery data.

---

### Project Info

## Summary
This project develops a parallel application using MPI and C++ that computes a path across scientifically significant zones on the lunar surface, using data from the Lunar Reconnaissance Orbiter. The application leverages a greedy algorithm and A* pathfinding adapted for parallel execution, aimed at providing rapid, efficient route calculations during lunar missions.

## Key Components
- **Node:** Represents points on a grid with costs, heuristics, and navigational data.
- **Grid:** A 2D array indicating traversable and blocked regions, essential for mapping the lunar surface.
- **routeMap:** A dynamic representation of the Grid, storing path-related data for navigation.
- **antennaList:** Dynamic locations for antenna placement, critical for maintaining communication during missions.
- **Priority Queue:** Utilized within A* to prioritize nodes based on cost and heuristic estimates for efficient pathfinding.

## Approach
Our approach involves vertical and horizontal parallelism to optimize pathfinding:
- **Vertical Parallelism:** Each processor handles a contiguous segment of rows, determining antenna placements and the shortest path to the segment's end.
- **Horizontal Parallelism:** Each processor operates on continuous columns, improving data locality and parallel efficiency.

See [Final Report](finalreport.pdf) (PDF) for full information on this project.

### Mid-Project Progress Report

#### Data Conversion with GDAL
We have successfully configured our project to convert Lunar Reconnaissance Orbiter (LRO) files, which are in `.img` and `.image` formats, into usable data formats for our program. This conversion is made feasible by utilizing the Geospatial Data Abstraction Library (GDAL), a versatile C++ library capable of reading and writing a broad array of raster and vector geospatial data formats. Our use of GDAL simplifies the process of obtaining slope maps and visual data. We are exploring the potential of GDAL for obstacle detection; if suitable LRO files are unavailable for existing crater and rock maps, we may employ an off-the-shelf machine learning algorithm to pre-analyze all surface imagery for obstacle identification.

#### Project Design Readjustments for Enhanced Parallelization
We've implemented several design changes to enhance parallel processing capabilities within our project. Initially, we are processing larger images at a lower resolution to swiftly establish a general path, significantly reducing the immediate data handling requirements. Our system is set up to preprocess this data in parallel, aiming to accelerate our computations significantly.

For the A* algorithm, we have developed a version that can operate in parallel. Currently, it functions sequentially, but we plan to modify this by segmenting the map into sections that can be processed simultaneously. This strategy includes domain decomposition—dividing the lunar map into segments processed concurrently—and parallel frontier expansion within the A* search tree. This expansion allows multiple processors to efficiently extend search frontiers.

#### Schedule Adjustments
Our progress was initially slowed due to our involvement in Carnival week, where we engaged in activities for Lunar Robotics, among other commitments. Consequently, we have refocused our efforts on core functionalities—specifically the parallelization of tasks—rather than on developing a graphical user interface (GUI). The 'zooming' feature, which would allow us to selectively focus on pertinent sections of high-resolution images, remains an optional optimization. Our primary objective now is to ensure effective parallelism using MPI across both image processing and A* analysis.