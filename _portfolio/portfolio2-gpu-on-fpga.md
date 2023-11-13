---
title: "OpenGL GPU on a Xilinx FPGA"
excerpt: "Exploring graphics architecture by building a graphics pipeline capable of executing simple OpenGL programs<br/><img src='/images/Projects/fpga_gpu/fpga overview.png'>"
collection: portfolio
---

# Overview
This project was completed as part of CPRE 480 (Computer Graphics Architecture) at Iowa State University taught by Dr. Joseph Zambreno during the Spring of 2021. This was a course-long project where I worked on a team with Margaret Heaslip, Ryan Lanciloti, and Daniel Shaw. I proceeded to act as a teaching assistant for this course in the Spring of 2022 where I was awarded a teaching excellence award for my efforts with this course and an undergraduate course I simultaneously TA'd.

The goal of this course-long project was to build the simple graphics pipeline on a Xilinx Nexys Video Artix-7 FPGA. We were responsible for the implementation and verification of the graphics pipeline components as well as the driver code used to control the FPGA from the host PC.

# Communicating with the FPGA
Our FPGA communicated with the host PC over ethernet using the UDP communication protocol. The FPGA would perform DMA writes and reads from the available memory utilizing the AXI protocol. The host driver would configure the FPGA correctly through control registers within individual components and set any necessary memory regions such as the SPIR-V assembly for shaders.

# The GPU Design
The GPU followed the simple graphics pipeline which flowed in the following order:
1. VertexFetch
2. VertexShading
3. ViewportTransformation
4. Rasterization
5. FragmentShading
6. RenderOutput

![image](/images/Projects/fpga_gpu/graphics_subsytem.png)

# Conclusion and Future Work
The resulting FPGA design was capable of running an OpenGL application that utilized vertex and fragment shading. We did not run formal performance evaluations on our design and the overall performance is admittedly rather limited due to the linear execution of our design. Parallelizing the design would greatly speed up the design.

In the future, I hope to re-implement this design on a Xilinx Ultrascale+ SoC. The goal would be to deploy the GPU on the PL and have Linux running through the PS. This design would communicate utilizing the AXI protocol directly rather than ethernet reducing overhead. Additionally, I hope to parallelize the design. With the move to Linux and the ARM architecture, the GPU core will need to be rewritten to utilize OpenGL-ES or Vulkan which is another planned change. A Vulkan implementation seems particularly interesting as I can directly program the design for both GPGPU and graphics applications.