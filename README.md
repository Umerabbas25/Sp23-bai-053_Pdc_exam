# PDC MID LAB - Image Processing Performance Analysis

This repository contains implementations of sequential, parallel, and distributed image processing approaches for analyzing performance improvements in computer vision tasks.

## Project Overview

The project processes 94 images across 4 classes (cars, cats, dogs, flowers) using different computational approaches:
- **Sequential Processing**: Single-threaded image processing
- **Parallel Processing**: Multi-threaded processing with configurable worker counts
- **Distributed Processing**: Multi-process simulation of distributed computing

## Files Structure

```
PDC_MID_LAB/
├── images_dataset/           # Input images organized by class
│   ├── cars/                # 21 car images
│   ├── cats/                # 23 cat images  
│   ├── dogs/                # 23 dog images
│   └── flowers/             # 27 flower images
├── sequential_process.py    # Sequential image processing implementation
├── parallel_process.py      # Parallel processing with ThreadPoolExecutor
├── distributed_process.py   # Distributed processing simulation
├── report.txt               # Performance analysis report
└── README.md               # This file
```

## Image Processing Pipeline

Each image undergoes the following processing steps:
1. **Load**: Read image using OpenCV
2. **Resize**: Scale to 128x128 pixels
3. **Watermark**: Add "PDC_LAB" watermark
4. **Save**: Write processed image to output directory

## Performance Results

| Processing Method | Time (seconds) | Speedup | Images Processed |
|------------------|----------------|---------|------------------|
| Sequential       | 1.49           | 1.00x   | 94/94           |
| Parallel (8 workers) | 0.07        | 21.29x  | 94/94           |
| Distributed (2 nodes) | 0.12     | 12.42x  | 94/94           |

### Parallel Processing Speedup Analysis
| Workers | Time (s) | Speedup |
|---------|----------|---------|
| 1       | 0.21     | 1.00x   |
| 2       | 0.13     | 1.67x   |
| 4       | 0.09     | 2.41x   |
| 8       | 0.07     | 3.10x   |

## Requirements

- Python 3.11
- OpenCV (`opencv-python`)
- Standard library modules: `os`, `time`, `multiprocessing`, `concurrent.futures`

## Installation

```bash
# Clone the repository
git clone <repository-url>
cd PDC_MID_LAB

# Install required packages
pip install opencv-python

# Ensure images_dataset folder exists with images
```

## Usage

### Sequential Processing
```bash
python sequential_process.py
```
Output: `output_seq/` directory with processed images

### Parallel Processing
```bash
python parallel_process.py
```
Output: `output_parallel/` directory with processed images and performance table

### Distributed Processing
```bash
python distributed_process.py
```
Output: `output_distributed/` directory with processed images and node performance

## Key Findings

### Optimal Configuration: 8 Workers
The best performance was achieved with 8 workers, providing a 3.10x speedup over single-threaded parallel processing and 21.29x speedup over sequential processing.

### Performance Analysis
- **Sequential**: 1.49 seconds (baseline)
- **Parallel (8 workers)**: 0.07 seconds (21.29x speedup)
- **Distributed (2 nodes)**: 0.12 seconds (12.42x speedup)

### Bottlenecks Identified
1. **I/O Operations**: Disk read/write remains the primary bottleneck
2. **Memory Bandwidth**: Multiple threads competing for memory access
3. **Storage Device Speed**: Hardware limitations on concurrent file operations
4. **Context Switching**: Overhead increases beyond optimal worker count

## Technical Implementation

### Sequential Processing
- Single-threaded execution
- Processes images one after another
- Simple and reliable approach

### Parallel Processing
- Uses `ThreadPoolExecutor` for concurrent execution
- Configurable worker count (1, 2, 4, 8 workers)
- Automatic cleanup and result aggregation

### Distributed Processing
- Uses `multiprocessing.Process` for separate processes
- Simulates 2-node distributed environment
- Equal task distribution between nodes

## Performance Insights

1. **Parallelism Benefits**: Significant performance improvement through concurrent processing
2. **Diminishing Returns**: Performance gains plateau beyond optimal worker count
3. **I/O Bottleneck**: Storage operations remain the limiting factor
4. **Resource Utilization**: Better CPU and memory utilization with parallel approaches

## Report

Detailed analysis available in `report.pdf` including:
- Performance comparison tables
- Bottleneck analysis
- Technical implementation details
- Conclusions and recommendations
