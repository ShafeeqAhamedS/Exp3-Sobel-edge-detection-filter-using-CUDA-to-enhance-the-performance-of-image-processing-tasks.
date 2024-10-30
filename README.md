# Sobel edge detection filter using CUDA to enhance the performance of image processing tasks

### EX. NO: 03
### ENTER YOUR NAME: Shafeeq Ahamed S
### REGISTER NO: 212221230092
### DATE:

## Background: 
  - The Sobel operator is a popular edge detection method that computes the gradient of the image intensity at each pixel. It uses convolution with two kernels to determine the gradient in both the x and y directions. 
  - This lab focuses on utilizing CUDA to parallelize the Sobel filter implementation for efficient processing of images.

## Aim
To utilize CUDA to parallelize the Sobel filter implementation for efficient processing of images.

## Tools Required:
- A system with CUDA-capable GPU.
- CUDA Toolkit and OpenCV installed.
- A sample image for testing.

## Procedure

1. **Environment Setup**:
   - Ensure that CUDA and OpenCV are installed and set up correctly on your system.
   - Have a sample image (`images.jpg`) available in the correct directory to use as input.

2. **Load Image and Convert to Grayscale**:
   - Use OpenCV to read the input image in color mode.
   - Convert the image to grayscale as the Sobel operator works on single-channel images.

3. **Initialize and Allocate Memory**:
   - Determine the width and height of the grayscale image.
   - Allocate memory on both the host (CPU) and device (GPU) for the image data. Allocate device memory using `cudaMalloc` and check for successful allocation with `checkCudaErrors`.

4. **Performance Analysis Function**:
   - Define `analyzePerformance`, a function to test the CUDA kernel with different image sizes and block configurations.
   - For each specified image size (e.g., 256x256, 512x512, 1024x1024), set up the grid and block dimensions.
   - Launch the Sobel kernel using different block sizes (8x8, 16x16, 32x32) to evaluate the performance impact of each configuration. Record the execution time using CUDA events.

5. **Run Sobel Filter on Original Image**:
   - Set up the grid and block dimensions for the input image based on a 16x16 block size.
   - Use CUDA events to measure execution time for the Sobel filter applied to the original image.
   - Copy the resulting data from device memory to host memory.

6. **Save CUDA Output Image**:
   - Convert the processed image data on the host back to an OpenCV `Mat` object.
   - Save the CUDA-processed output image as `output_sobel_cuda.jpeg`.

7. **Compare with OpenCV Sobel Filter**:
   - For comparison, apply the OpenCV Sobel filter to the grayscale image on the CPU.
   - Measure the execution time using `std::chrono` for the CPU-based approach.
   - Save the OpenCV output as `output_sobel_opencv.jpeg`.

8. **Display Results**:
   - Print the input and output image dimensions.
   - Print the execution time for the CUDA Sobel filter and the CPU (OpenCV) Sobel filter to compare performance.
   - Display the breakdown of times for each block size and image size tested.

9. **Cleanup**:
   - Free all dynamically allocated memory on the host and device to avoid memory leaks.
   - Destroy CUDA events created for timing.


## Output Explanation

| Original 	|  Output using Cuda |
|:-:	|:-:	|
| ![image](https://github.com/user-attachments/assets/e7fa9849-d486-4669-bc6c-1f0bea126742) | ![image](https://github.com/user-attachments/assets/2a5b6bd2-cd38-419f-bed4-f06ca45d6a76) |

| Original 	|  Output using OpenCV |
|:-:	|:-:	|
| ![image](https://github.com/user-attachments/assets/e7fa9849-d486-4669-bc6c-1f0bea126742) |  ![image](https://github.com/user-attachments/assets/7ce4e5eb-5de7-44a0-8142-3c7d1c9ecc13) |

- **Sample Execution Results**:
  - **CUDA Execution Times (Sobel filter)**
  </br>

![image](https://github.com/user-attachments/assets/bc4f2f40-2f6c-4dd8-af8b-e4583b28079d)


  - **OpenCV Execution Time**
  </br>

![image](https://github.com/user-attachments/assets/db287c68-1ae8-42a4-9ef3-a78f16d0de37)

- **Graph Analysis**:
  - Displayed a graph showing the relationship between image size, block size, and execution time.
 </br>

 ![image](https://github.com/user-attachments/assets/ddb5fb05-53fe-440f-8876-0d3797de1bb5)


## Answers to Questions

1. **Challenges Implementing Sobel for Color Images**:
   - Converting images to grayscale in the kernel increased complexity. Memory management and ensuring correct indexing for color to grayscale conversion required attention.

2. **Influence of Block Size**:
   - Smaller block sizes (e.g., 8x8) were efficient for smaller images but less so for larger ones, where larger blocks (e.g., 32x32) reduced overhead.

3. **CUDA vs. CPU Output Differences**:
   - The CUDA implementation was faster, with minor variations in edge sharpness due to rounding differences. CPU output took significantly more time than the GPU.

4. **Optimization Suggestions**:
   - Use shared memory in the CUDA kernel to reduce global memory access times.
   - Experiment with adaptive block sizes for larger images.
   - Consider overlapping memory transfer and kernel execution.

## Result
Successfully implemented a CUDA-accelerated Sobel filter, demonstrating significant performance improvement over the CPU-based implementation, with an efficient parallelized approach for edge detection in image processing.
