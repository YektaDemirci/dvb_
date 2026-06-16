# SNS-3 Satellite Simulation Setup

This repository contains the setup guide for running **SNS-3** simulations. It is based on the official guidelines from the [SNS-3 Satellite GitHub Repository](https://github.com/sns3/sns3-satellite).

To run an SNS-3 simulation, you need to clone and configure **four specific repositories** at compatible commit versions.

---

## Directory Structure

The supporter repositories must be cloned inside the `contrib/` folder of your base `ns-3-dev` directory. Your final folder structure should look exactly like this:

```text
your_folders/
└── ns-3-dev/                     # Base Repository
    └── contrib/
        ├── magister-stats/       # Supporter Repository
        ├── satellite/            # Supporter Repository
        └── traffic/              # Supporter Repository     
```

# A. Clone the base ns-3 repository, checkout go to contrib
```bash
git clone https://gitlab.com/nsnam/ns-3-dev.git
cd ns-3-dev
git checkout ea50b72ab79b1ec5912c66d5b384effa829f18bc
cd contrib
```

## --- 1. Clone and Checkout 'satellite' ---
```bash
git clone https://github.com/sns3/sns3-satellite.git satellite
cd satellite && git checkout c4c6e604c3e71daa30c5331d3bbef47b03770deb && cd ..
```

## --- 2. Clone and Checkout 'traffic' ---
```bash
git clone https://github.com/sns3/traffic.git traffic
cd traffic && git checkout 2710ed71c2cba9d92940bdf53ad85159504329d9 && cd ..
```

## --- 3. Clone and Checkout 'magister-stats' ---
```bash
git clone https://github.com/sns3/stats.git magister-stats
cd magister-stats && git checkout 003f6a29ce74808d0b2579fd16a9718f793f5bfe && cd ..
```

Once you have these, you can compile the source codes as described by [SNS-3 CMake](https://github.com/sns3/sns3-satellite#cmake).
If the compilation is successful you should be able to run the default simulation examples, for instance:

```bash
./ns3 run sat-fwd-link-beam-hopping-example
```


# B. Enabling Dynamic Beam Hopping

The default commits do not support dynamic beam hopping out of the box. To enable this feature, you can use the scripts provided in this repository by placing them in the correct directories as outlined below.

### 1. Example Script
Refer to the primary example script for dynamic beam hopping:
* **File:** `sat-fwd-link-beam-hopping-example_2.cc`
* **Target Location:** `.../contrib/satellite/examples/`

### 2. Model Files
The implementation relies on two core model files that must be added to the simulation engine:
* **Files:** `satellite-dynamic-bstp.cc` and `satellite-dynamic-bstp.h`
* **Target Location:** `.../contrib/satellite/model/`

### 3. Demand Forecasting Scripts
Finally, include the python-based demand forecasting scripts required for the simulation:
* **Files:** `far.py` and `fgn.py`
* **Target Location:** `.../contrib/satellite/examples/`
