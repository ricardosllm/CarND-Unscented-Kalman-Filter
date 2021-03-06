# CarND-Unscented-Kalman-Filter

Self-Driving Car Engineer Nanodegree Program

The goal of this project is to build an Unscented Kalman Filter using C++ and
use it to estimate the state of a moving object of interest with noisy LIDAR
and RADAR measurements.

The measurements data is provided in the form of a [simulator](https://github.com/udacity/self-driving-car-sim/releases).

The key metrics are [RMSE](https://en.wikipedia.org/wiki/Root-mean-square_deviation) values for both position and velocity of the tracked
object.

## Results

The success metrics for this project are the RMSE values.

The values shoule be below:
- `0.09` for `P x`,
- `0.10` for `P y`,
- `0.40` for `V x`,
- `0.30` for `V y`.

### RMSE values

The folowing table lists the results of both datasets:

| RMSE | Dataset 1 |
|------|-----------|
| P x  |  0.0606247   |
| P y  |  0.0860925   |
| V x  |  0.329898   |
| V y  |  0.213063   |

As we can see the results are below the desired values indicating a **successful Unscented Kalman Filter implementation**.

#### Using only one senor

A run with only one sensor, `radar` or `lidar` was also measured.

> You can test this yourself by setting the vars `use_laser_` and `use_radar_` in `src/ukf.cpp`.

Here are the results:

##### Dataset 1

| RMSE | only RADAR | only LIDAR |
|------|-----------|-----------|
| P x  |  0.155448   |  0.100553   |
| P y  |  0.200174   |  0.0981127   |
| V x  |  0.362301   |  0.60588   |
| V y  |  0.320537   |  0.238563   |

Interesting points here:
- With only `Radar` data the results are worse then with both sensors but quite similar in terms of velocity `Vx`.
- With only `Lidar` data the position `Px` and `Py` are far better then with only `Radar`, velocity `Vx` is 2x worse and `Vy` is ~30% better
- Overall the performance with a single sensor is worse than with both, as we would expect.

### Images from the simulator

> With both `Radar` and `Lidar` data.

#### Dataset 1

![alt text](results/UKF-dataset-1.png "Dataset 1")

> The red and blue dots are the Radar and Lidar measurements and the green dots the predicted position.

## Implementation

The code skeleton for this project was provided by udacity on [this repo](https://github.com/udacity/CarND-Unscented-Kalman-Filter-Project).

The main program in under the `src` directory.
```
.
├── json.hpp
├── main.cpp
├── measurement_package.h
├── tools.cpp
├── tools.h
├── ukf.cpp
└── ukf.h
```

The main changes were to the folowing files:
- `ukf.cpp` - initializes the Unscented Kalman filter, calls the predict and update function, defines the predict and update functions
- `tools.cpp` - function to calculate RMSE

### Unit tests

The code is not tested at the moment, this is somthing I want to add in the future using [Google's gTest](https://github.com/google/googletest) framework.

---

# Contributing

## Dependencies

* cmake >= 3.5
  * All OSes: [click here for installation instructions](https://cmake.org/install/)
* make >= 4.1 (Linux, Mac), 3.81 (Windows)
  * Linux: make is installed by default on most Linux distros
  * Mac: [install Xcode command line tools to get make](https://developer.apple.com/xcode/features/)
  * Windows: [Click here for installation instructions](http://gnuwin32.sourceforge.net/packages/make.htm)
* gcc/g++ >= 5.4
  * Linux: gcc / g++ is installed by default on most Linux distros
  * Mac: same deal as make - [install Xcode command line tools](https://developer.apple.com/xcode/features/)
  * Windows: recommend using [MinGW](http://www.mingw.org/)

## Build

1. Clone this repo.
2. Make a build directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
   * On windows, you may need to run: `cmake .. -G "Unix Makefiles" && make`
4. Run it: `./UnscentedKF` Previous versions use i/o from text files.  The current state uses i/o

## Editor Settings

We've purposefully kept editor configuration files out of this repo in order to
keep it as simple and environment agnostic as possible. However, we recommend
using the following settings:

* indent using spaces
* set tab width to 2 spaces (keeps the matrices in source code aligned)

## Code Style

Please (do your best to) stick to [Google's C++ style guide](https://google.github.io/styleguide/cppguide.html).


