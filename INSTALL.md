# Installation Guide

Complete setup instructions for Computer Graphics Algorithms project.

## System Requirements

- **Compiler**: GCC 7.0+, Clang 5.0+, MSVC 2015+
- **Build Tools**: Make or CMake
- **Graphics API**: OpenGL 2.1+ support
- **Memory**: 512 MB minimum
- **Disk Space**: 100 MB

## Platform-Specific Setup

### Windows (MinGW)

#### Using MinGW Package Manager
```bash
# Install MinGW GCC and FreeGLUT
pacman -S mingw-w64-x86_64-gcc mingw-w64-x86_64-freeglut

# Verify installation
gcc --version
```

#### Using MSVC
```bash
# Download GLUT from: https://www.opengl.org/resources/libraries/glut/
# Extract to your VC++ directory:
# - glut.h → include/GL/
# - glut.lib → lib/
# - glut.dll → System32/
```

#### Compilation (MinGW)
```bash
g++ -o program program.cpp -lGL -lGLU -lglut
```

### Linux (Ubuntu/Debian)

```bash
# Update package lists
sudo apt-get update

# Install required packages
sudo apt-get install build-essential freeglut3-dev libglew-dev

# Install optional tools
sudo apt-get install cmake git

# Verify installation
g++ --version
```

#### Compilation
```bash
g++ -o program program.cpp -lGL -lGLU -lglut

# Run
./program
```

### Linux (Fedora/RHEL)

```bash
# Install required packages
sudo dnf install gcc-c++ freeglut-devel glew-devel

# Verify
g++ --version
```

### macOS

#### Using Homebrew
```bash
# Install Homebrew if not present
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Install FreeGLUT
brew install freeglut

# Install optional tools
brew install cmake
```

#### Using System OpenGL (Built-in)
```bash
# macOS includes OpenGL framework
# Just need to link it during compilation
g++ -o program program.cpp -framework OpenGL -framework GLUT
```

#### Compilation
```bash
# Using system frameworks
g++ -o program program.cpp -framework OpenGL -framework GLUT

# Or with Homebrew FreeGLUT
g++ -o program program.cpp -I/usr/local/include -L/usr/local/lib -lglut -lGL -lGLU
```

## Build Methods

### Method 1: Direct Compilation (Simplest)

```bash
# Single file compilation
g++ -o output_name source.cpp -lGL -lGLU -lglut

# Multiple files
g++ -o output_name file1.cpp file2.cpp -lGL -lGLU -lglut

# With optimization
g++ -O2 -o output_name source.cpp -lGL -lGLU -lglut

# With debugging symbols
g++ -g -o output_name source.cpp -lGL -lGLU -lglut
```

### Method 2: Makefile (Recommended)

Create `Makefile` in project root:

```makefile
# Variables
CXX = g++
CXXFLAGS = -Wall -std=c++11 -O2
LIBS = -lGL -lGLU -lglut
BIN_DIR = bin
SRC_DIR = PE

# Targets
all: $(BIN_DIR)/dda_home $(BIN_DIR)/bresenham_circle $(BIN_DIR)/cube

# DDA Home
$(BIN_DIR)/dda_home: $(SRC_DIR)/30by30/DDA_Home.cpp
	@mkdir -p $(BIN_DIR)
	$(CXX) $(CXXFLAGS) -o $@ $< $(LIBS)

# Bresenham Circle
$(BIN_DIR)/bresenham_circle: $(SRC_DIR)/30by30/practical_2.1_circle.cpp
	@mkdir -p $(BIN_DIR)
	$(CXX) $(CXXFLAGS) -o $@ $< $(LIBS)

# 3D Cube
$(BIN_DIR)/cube: $(SRC_DIR)/CG_IMP/CubeRY.txt
	@mkdir -p $(BIN_DIR)
	$(CXX) $(CXXFLAGS) -o $@ $< $(LIBS)

# Run target
run: all
	./$(BIN_DIR)/dda_home

# Clean build artifacts
clean:
	rm -rf $(BIN_DIR)/*.o
	rm -rf $(BIN_DIR)/

.PHONY: all run clean
```

Usage:
```bash
make all          # Compile all programs
make run          # Compile and run
make clean        # Remove binaries
```

### Method 3: CMake Build System

Create `CMakeLists.txt`:

```cmake
cmake_minimum_required(VERSION 3.10)
project(ComputerGraphics)

set(CMAKE_CXX_STANDARD 11)

# Find OpenGL and GLUT
find_package(OpenGL REQUIRED)
find_package(GLUT REQUIRED)

# Include directories
include_directories(${OPENGL_INCLUDE_DIR} ${GLUT_INCLUDE_DIR})

# Add executables
add_executable(dda_home PE/30by30/DDA_Home.cpp)
target_link_libraries(dda_home ${OPENGL_LIBRARIES} ${GLUT_LIBRARY})

add_executable(bresenham_circle PE/30by30/practical_2.1_circle.cpp)
target_link_libraries(bresenham_circle ${OPENGL_LIBRARIES} ${GLUT_LIBRARY})

# Add more executables as needed
```

Build:
```bash
mkdir build
cd build
cmake ..
make
./dda_home
```

## Troubleshooting

### "fatal error: GL/glut.h: No such file or directory"
**Solution**: Install GLUT development headers
```bash
# Ubuntu/Debian
sudo apt-get install freeglut3-dev

# Fedora/RHEL
sudo dnf install freeglut-devel

# macOS
brew install freeglut
```

### "undefined reference to `glutInit`"
**Solution**: Link GLUT library
```bash
g++ program.cpp -lglut -lGL -lGLU -o program
```

### "undefined reference to `glVertex3f`"
**Solution**: Link OpenGL library
```bash
g++ program.cpp -lGL -lglut -o program
```

### Windows: "cannot find -lglut"
**Solution**: Install MinGW GLUT or provide full path to libraries
```bash
pacman -S mingw-w64-x86_64-freeglut
```

### macOS: GLUT not found
**Solution**: Use framework links instead
```bash
g++ program.cpp -framework OpenGL -framework GLUT -o program
```

## Verification

Test your installation:

```cpp
// test_opengl.cpp
#include <GL/glut.h>
#include <iostream>

void display() {
    glClear(GL_COLOR_BUFFER_BIT);
    glFlush();
}

int main(int argc, char** argv) {
    std::cout << "OpenGL setup successful!" << std::endl;
    glutInit(&argc, argv);
    glutInitDisplayMode(GLUT_SINGLE | GLUT_RGB);
    glutInitWindowSize(400, 400);
    glutCreateWindow("Test");
    glutDisplayFunc(display);
    glutMainLoop();
    return 0;
}
```

Compile and run:
```bash
g++ test_opengl.cpp -lGL -lGLU -lglut -o test
./test
```

If a window appears, installation is successful!

## Next Steps

1. Navigate to project directory
2. Review [README.md](README.md) for project overview
3. Check [PE/30by30/README.md](PE/30by30/README.md) for practical exercises
4. Start with simple examples like DDA_Home.cpp
5. Progress to more complex algorithms

## Additional Resources

- [OpenGL Official Documentation](https://www.opengl.org/documentation/)
- [FreeGLUT Documentation](http://freeglut.sourceforge.net/docs/api.php)
- [CMake Documentation](https://cmake.org/cmake/help/latest/)
- [GNU Make Documentation](https://www.gnu.org/software/make/manual/)
