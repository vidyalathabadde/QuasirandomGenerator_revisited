# `BilateralFilter` Sample
 
 This sample uses OpenMP directives to perform a simple bilateral filter on an image and measures performance. The original OpenACC source code is migrated to OpenMP to Offload on Intel® Platforms.

| Area                  | Description
|:---                       |:---
| What you will learn       | Migrating and optimizing bilateralFilter from OpenACC to OpenMP
| Time to complete          | 15 minutes
| Category                  | Concepts and Functionality

## Purpose

Bilateral filter is an edge-preserving nonlinear smoothing filter. There are three parameters distribute to the filter: gaussian delta, euclidean delta and iterations.
When the euclidean delta increases, most of the fine texture will be filtered away, yet all contours are as crisp as in the original image. If the euclidean delta approximates to ∞, the filter becomes a normal gaussian filter. Fine texture will blur more with larger gaussian delta. Multiple iterations have the effect of flattening the colors in an image considerably, but without blurring edges, which produces a cartoon effect.

> **Note**: We use intel-application-migration-tool-for-openacc-to-openmp which assists developers in porting OpenACC code automatically to OpenMP code. 

This sample contains two versions in the following folders:

| Folder Name                   | Description
|:---                           |:---
| `src`              | Contains the original OpenACC source code 
| `OpenMP_migrated`            | Contains the OpenMP migrated code.

## Prerequisites

| Optimized for              | Description
|:---                        |:---
| OS                         | Ubuntu* 22.04
| Hardware                   | Intel® Data Center GPU Max
| Software                   | intel-application-migration-tool-for-openacc-to-openmp

For more information on how to install the above Tool, visit [intel-application-migration-tool-for-openacc-to-openmp](https://github.com/intel/intel-application-migration-tool-for-openacc-to-openmp)

## Key Implementation Details

This sample demonstrates the migration of the following OpenACC pragmas: 
- #pragma acc kernels \
          copyin()    \
          copyout()   \
          create()    \
          if()
- #pragma acc loop independent, gang


>  **Note**: Refer to [Portability across Heterogeneous Architectures](https://www.intel.com/content/www/us/en/developer/articles/technical/openmp-accelerator-offload.html#gs.n33nuz) for general information about the migration of OpenACC to OpenMP.

## Set Environment Variables

When working with the command-line interface (CLI), you should configure the oneAPI toolkits using environment variables. Set up your CLI environment by sourcing the `setvars` script every time you open a new terminal window. This practice ensures that the compiler, libraries, and tools are ready for development.

## Migrate the `bilateralFilter` Sample

### Migrate the Code using intel-application-migration-tool-for-openacc-to-openmp

For this sample, the tool takes application sources (either C/C++ or Fortran languages) with OpenACC constructs and generates a semantically-equivalent source using OpenMP. Follow these steps to migrate the code

  1. Tool installation
     ```
     https://github.com/intel/intel-application-migration-tool-for-openacc-to-openmp.git
     ```

The binary of the translator can be found inside intel-application-migration-tool-for-openacc-to-openmp/src location
    
  2. Change to the bilateralfilter sample directory.
     ```
     cd src/bilateralFilter/
     ```
  4. Now invoke the translator to migrate the openACC pragmas to OpenMP as shown below
     ```
     intel-application-migration-tool-for-openacc-to-openmp/src/intel-application-migration-tool-for-openacc-to-openmp bilateralFilter.c
     ```
### Optimizations
ca

## Build the `bilateralFilter` Sample for CPU and GPU

> **Note**: If you have not already done so, set up your CLI
> environment by sourcing  the `setvars` script in the root of your oneAPI installation.
>
> Linux*:
> - For system wide installations: `. /opt/intel/oneapi/setvars.sh`
> - For private installations: ` . ~/intel/oneapi/setvars.sh`
> - For non-POSIX shells, like csh, use the following command: `bash -c 'source <install-dir>/setvars.sh ; exec csh'`
>
> For more information on configuring environment variables, see [Use the setvars Script with Linux* or macOS*](https://www.intel.com/content/www/us/en/develop/documentation/oneapi-programming-guide/top/oneapi-development-environment-setup/use-the-setvars-script-with-linux-or-macos.html).

### On Linux*

1. Change to the sample directory.
2. Build the program.
   ```
   $ make
   ```
   
By default, this command sequence will build the `openMP_migrated_output ` version of the program.

3. Run the program.
   ```
   make run
   ```  
   
#### Troubleshooting

If an error occurs, you can get more details by running `make` with
the `VERBOSE=1` argument:
```
make VERBOSE=1
```
If you receive an error message, troubleshoot the problem using the **Diagnostics Utility for Intel® oneAPI Toolkits**. The diagnostic utility provides configuration and system checks to help find missing dependencies, permissions errors, and other issues. See the [Diagnostics Utility for Intel® oneAPI Toolkits User Guide](https://www.intel.com/content/www/us/en/docs/oneapi/user-guide-diagnostic-utility/2024-0/overview.html) for more information on using the utility.

## License
Code samples are licensed under the MIT license. See
[License.txt](https://github.com/oneapi-src/oneAPI-samples/blob/master/License.txt) for details.

Third party program licenses are at [third-party-programs.txt](https://github.com/oneapi-src/oneAPI-samples/blob/master/third-party-programs.txt).
