find_package(OpenCV REQUIRED)
add_executable(Rasterizer main.cpp rasterizer.hpp rasterizer.cpp Triangle.hpp Triangle.cpp)
target_link_libraries(Rasterizer PRIVATE Eigen3::Eigen ${OpenCV_LIBRARIES})
