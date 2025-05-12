====================
FlexiNeck Documentation
====================

Overview
--------

FlexiNeck is a highly configurable neural network neck module designed for computer vision tasks such as object detection, segmentation, and classification. It provides a flexible architecture that can be easily adapted to different backbone networks and task requirements.

Installation
------------

.. code-block:: bash

   pip install torch

Quick Start
-----------

Basic Usage
~~~~~~~~~~~

.. code-block:: python

   from flexineck import FlexiNeck

   # Define input channels from your backbone network
   in_channels = [256, 512, 1024, 2048]  # Typical ResNet backbone output

   # Create a neck for object detection
   neck_detection = FlexiNeck(
       in_channels=in_channels,
       out_channels=256,
       use_fpn=True,
       use_pan=True,
       use_spp=True,
       output_format="pyramid"
   )

Key Features
------------

- **Modular Design**: Easily configurable for different vision tasks
- **Multiple Feature Processing Techniques**:
  
  * Feature Pyramid Network (FPN)
  * Path Aggregation Network (PAN)
  * Spatial Pyramid Pooling (SPP)

- **Attention Mechanisms**:
  
  * Channel Attention
  * Spatial Attention
  * Hybrid Attention

- **Flexible Output Formats**:
  
  * Single Output
  * Multi-scale Output
  * Pyramid Output

Configuration Parameters
-----------------------

Main Parameters
~~~~~~~~~~~~~~~

.. list-table::
   :widths: 20 15 50 15
   :header-rows: 1

   * - Parameter
     - Type
     - Description
     - Default
   * - ``in_channels``
     - ``List[int]``
     - Input channel dimensions from backbone
     - Required
   * - ``out_channels``
     - ``int``
     - Number of output channels
     - 256
   * - ``use_fpn``
     - ``bool``
     - Enable Feature Pyramid Network
     - ``True``
   * - ``use_pan``
     - ``bool``
     - Enable Path Aggregation Network
     - ``True``
   * - ``use_spp``
     - ``bool``
     - Enable Spatial Pyramid Pooling
     - ``True``
   * - ``use_attention``
     - ``bool``
     - Enable attention mechanism
     - ``True``
   * - ``attention_type``
     - ``str``
     - Type of attention ("channel", "spatial", "hybrid")
     - "channel"
   * - ``fusion_type``
     - ``str``
     - Feature fusion method
     - "adaptive"
   * - ``output_format``
     - ``str``
     - Output format ("single", "multi_scale", "pyramid")
     - "multi_scale"

Attention Mechanisms
-------------------

Channel Attention
~~~~~~~~~~~~~~~~~

- Learns channel-wise importance
- Uses both average and max pooling
- Reduces computational complexity

Spatial Attention
~~~~~~~~~~~~~~~~~

- Focuses on important spatial regions
- Combines channel-wise mean and max

Hybrid Attention
~~~~~~~~~~~~~~~~

- Combines both channel and spatial attention
- Provides more comprehensive feature refinement

Output Formats
--------------

Single Output
~~~~~~~~~~~~~

- Concatenates and processes features into a single tensor
- Useful for tasks requiring a unified feature representation

Multi-scale Output
~~~~~~~~~~~~~~~~~~

- Returns features at different scales
- Preserves multi-resolution information

Pyramid Output
~~~~~~~~~~~~~~

- Returns a dictionary of features
- Directly usable in detection frameworks

Architecture
------------

.. image::  WhatsApp Image 2025-05-12 à 16.30.09_e9bba167.jpg
   :alt: FlexiNeck Architecture Diagram
   :align: center

Key Components
~~~~~~~~~~~~~~

- **Lateral Convolutions**: Project input features to a consistent channel dimension
- **Feature Pyramid Network (FPN)**: Top-down pathway for feature enhancement
- **Path Aggregation Network (PAN)**: Bottom-up pathway for additional feature refinement
- **Spatial Pyramid Pooling (SPP)**: Multi-scale feature extraction
- **Attention Modules**: Adaptive feature refinement
- **Fusion Modules**: Combining features with learnable weights

Advanced Usage Examples
----------------------

Object Detection Configuration
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: python

   neck_detection = FlexiNeck(
       in_channels=[256, 512, 1024, 2048],
       out_channels=256,
       use_fpn=True,
       use_pan=True,
       use_spp=True,
       attention_type="channel",
       output_format="pyramid"
   )

Segmentation Configuration
~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: python

   neck_segmentation = FlexiNeck(
       in_channels=[256, 512, 1024, 2048],
       out_channels=256,
       use_fpn=True,
       use_pan=False,
       use_spp=True,
       attention_type="hybrid",
       output_format="single",
       output_size=(128, 128)
   )

Performance Considerations
-------------------------

- **Computational Overhead**: Additional modules increase computational complexity
- **Memory Usage**: Multiple attention and fusion modules require more memory
- **Recommended Hardware**: GPU with sufficient VRAM

Limitations
-----------

- Requires careful tuning for optimal performance
- May not be optimal for all vision tasks
- Performance depends on backbone network

Contributing
------------

Contributions are welcome! Please submit pull requests or open issues on our GitHub repository.

License
-------

[Insert your project's license information]

References
----------

1. Feature Pyramid Networks for Object Detection
2. Path Aggregation Network for Instance Segmentation
3. Spatial Pyramid Pooling in Deep Convolutional Networks for Visual Recognition
