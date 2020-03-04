# codeblocks-opencv
Build openCV based on Codeblocks
搬运自:  https://medium.com/@sourabhjigjinni/install-opencv-4-0-0-for-c-windows-7-10-code-blocks-tdm-gcc-64-dff65addf162

[toc]

# Abstract

This is a step-by-step installation of OpenCV 4.1.0 on Windows. I was inspired to make this installation guide to help people avoid the stress I went through to install this on windows. I have obviously installed this myself with the help of other people’s slightly older blogs. Thanks to [Zahid Hasan for the guide on version 3.2.0](https://zahidhasan.github.io/2017-03-25-How-to-install-OpenCV-3.2-in-windows-10-using-MinGW-(64)-and-Codeblocks/) which most of this is based on.

# **1. Install Code::Blocks**

![image-20200304105221358](C:\Users\xrc\AppData\Roaming\Typora\typora-user-images\image-20200304105221358.png)

Download [Code::Blocks](http://www.codeblocks.org/downloads/26) here or google codeblocks > downloads > Download the binary Release.

Click on the **sourceforge.net** link for the *codeblocks-17.12-setup.exe* option as we want to use TDM (64 bit) compiler.

# **2. Install TDM-GCC**

Download [TDM-GCC](http://tdm-gcc.tdragon.net/download) here. Make sure to select the 64 bit version.

![image-20200304105422952](C:\Users\xrc\AppData\Roaming\Typora\typora-user-images\image-20200304105422952.png)

Install it in C:\ drive. it will look like C:\TDM-GCC-64\. The bin folder should be registered automatically in system path during the installation process

<img src="C:\Users\xrc\AppData\Roaming\Typora\typora-user-images\image-20200304110033173.png" alt="image-20200304110033173" style="zoom:75%;" /> <img src="C:\Users\xrc\AppData\Roaming\Typora\typora-user-images\image-20200304110105856.png" alt="image-20200304110105856" style="zoom:75%;" />

# 3. Download the source of OpenCV 4.1.0

Download [OpenCV 4.1.0](https://opencv.org/releases.html) and click sources to get the zip/excute file.

Create folders:

- C:\opencv\source\
- C:\opencv\build\

![image-20200304110732682](C:\Users\xrc\AppData\Roaming\Typora\typora-user-images\image-20200304110732682.png)

# 4. Install CMake

Download [CMake](https://cmake.org/download/) and install.

![image-20200304111255767](C:\Users\xrc\AppData\Roaming\Typora\typora-user-images\image-20200304111255767.png)

# 5. Build the Binaries

1. Open cmake, set source path to C:\opencv\source\ and binary path to C:\opencv\build.
2. Click configure
3. Choose CodeBlock — MinGW Makefiles (Should be set by default)

<img src="C:\Users\xrc\AppData\Roaming\Typora\typora-user-images\image-20200304113728230.png" alt="image-20200304113728230" style="zoom:80%;" />

After configuring you will see options in red. We need to disable some of these to build the system:

- disable WITH_MFMS (media foundation needs special win sdk, only available for VS)
- ENABLE_PRECOMPILED_HEADERS=OFF
- WITH_IPP=OFF WITH_TBB=OFF (again libs available are for VS only)

MAKE SURE

- WITH_MFMS=OFF
- WITH_IPP=OFF,
- WITH_TBB=OFF
- ENABLE_PRECOMPILED_HEADERS=OFF

And

- WITH_OPENCL=ON
- WITH_OPENCL_D3D11_NV=OFF
- WITH_DIRECTX=ON

Lastly

- BUILD_PROTOBUF = OFF
- PROTOBUF_UPDATE_FILES = OFF
- WITH_PROTOBUF = OFF

Next click Generate.

1. You will find a codeblocks project file (opencv.cbp) in C:\opencv\build folder. Just double click it and codeblocks should load it. If it doesn’t just find the codeblocks app and open it.
2. Go to ‘*settings*‘, choose ‘*compiler’ and c*lick ‘*Toolchain executable*‘. In the ‘*compiler’s installation directory*‘ field choose the “*bin*” folder of MinGW C:\TDM-GCC-64\bin. set the following:

- c compile: gcc.exe

- c++ compiler: g++.exe

- Linker for dynamic libs: ar.exe

![image-20200304113851306](C:\Users\xrc\AppData\Roaming\Typora\typora-user-images\image-20200304113851306.png)

3. DONT BUILD TARGET IN A HURRY, this is where I went wrong, while following Zahid Hasan’s article. Select build > select target > install

![image-20200304113938739](C:\Users\xrc\AppData\Roaming\Typora\typora-user-images\image-20200304113938739.png)

4. After this step you can build.

Tip: the percentage of the build done is shown here. This will take a while depending on your hardware. It took me 1.5 hours.

\5. Add ***C:\opencv\build\install\x64\mingw\bin\*** to the path.

- windows 7 — [video](https://youtu.be/NTH03BSTj_Y)
- windows 10 — [link](https://www.architectryan.com/2018/03/17/add-to-the-path-on-windows-10/)

Tip: you can check path variables with **echo %path:;=&echo.%** in command prompt.

# 6. Run a C++ test program

1. Create a test project in Code::Blocks. Select console application.
2. Go to settings -> compiler. Select ‘search directories’ and in the ‘compiler’ tab chose the followings:

- C:\opencv\build\install\include
- C:\opencv\build\install\include\opencv2

![image-20200304114030196](C:\Users\xrc\AppData\Roaming\Typora\typora-user-images\image-20200304114030196.png)

3. Select ‘Linker’ tab and add C:\opencv\build\install\x64\mingw\lib

![image-20200304114101936](C:\Users\xrc\AppData\Roaming\Typora\typora-user-images\image-20200304114101936.png)

4. Go to ‘Linker Settings’ and add all the libraries from **C:\OpenCV\my_build\install\x64\mingw\lib** folder

   ![image-20200304114140489](C:\Users\xrc\AppData\Roaming\Typora\typora-user-images\image-20200304114140489.png)

   ![image-20200304114205831](C:\Users\xrc\AppData\Roaming\Typora\typora-user-images\image-20200304114205831.png)

   If it looks like this, all is good. Just one last step of using c++11 standard.

   ![image-20200304114239974](C:\Users\xrc\AppData\Roaming\Typora\typora-user-images\image-20200304114239974.png)

   5. Set the compiler to c++11 standard (Settings -> Compiler)

   ![image-20200304114319983](C:\Users\xrc\AppData\Roaming\Typora\typora-user-images\image-20200304114319983.png)

   6. Edit your main.cpp and add this:

   ```c++
   #include <iostream>
   #include <opencv2\highgui\highgui.hpp>
   #include <opencv2\opencv.hpp>
   
   using namespace std;
   using namespace cv;
   
   int main() {
   
   	VideoCapture cap(0);
   	if (!cap.isOpened()) {
   		cout << "Error initializing video camera!" << endl;
   		return -1;
   	}
   
   	char* windowName = "Webcam Feed";
   	namedWindow(windowName, WINDOW_AUTOSIZE);
   
   	while (1) {
   
   		Mat frame;
   		bool bSuccess = cap.read(frame);
   
   		if (!bSuccess) {
   			cout << "Error reading frame from camera feed" << endl;
   			break;
   		}
   
   		imshow(windowName, frame);
   		switch (waitKey(10)) {
   		case 27:
   			return 0;
   		}
   	}
   	return 0;
   }
   ```

   7. Build and run

   If u get an error like this restart your computer.

![image-20200304114434680](C:\Users\xrc\AppData\Roaming\Typora\typora-user-images\image-20200304114434680.png)

If your program compiles your webcam should start. If u don’t have a webcam try to [open an image](https://docs.opencv.org/2.4/doc/tutorials/introduction/display_image/display_image.html) with openCV. 
