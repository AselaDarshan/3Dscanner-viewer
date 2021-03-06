cmake_minimum_required (VERSION 2.8 FATAL_ERROR)
set( CMAKE_PREFIX_PATH  /usr/local)
project      (Visualizer)
#set  (VTK_DIR "/usr/local/include/vtk-6.2" CACHE PATH "VTK directory override" FORCE)
#set  (VTK_INCLUDE_DIRS )
#set  (VTK_LIBRARY_DIRS)
#set  (VTK_LIBRARY_DIRS /usr/local/lib/)
find_package (PCL 1.7.2 REQUIRED)
find_package (Qt4 REQUIRED)
find_package (VTK)

link_directories    (${PCL_LIBRARY_DIRS})
include_directories (${PCL_INCLUDE_DIRS})
add_definitions     (${PCL_DEFINITIONS})

set  (project_SOURCES main.cpp viewer.cpp connectionhelper.cpp connector.cpp)
set  (project_HEADERS viewer.h connectionhelper.h connector.h)
set  (project_FORMS   viewer.ui)
#set  (VTK_LIBRARIES   /usr/local/lib/libvtkGUISupportQt-6.2.so /usr/local/lib/libvtkCommonColor-6.2.so /usr/local/lib/libvtkRenderingCore-6.2.so /usr/local/lib/libvtkInteractionStyle-6.2.so.1 /usr/local/lib/libvtkRenderingFreeTypeOpenGL-6.2.so /usr/local/lib/libvtkRenderingFreeType-6.2.so.1 /usr/local/lib/libvtkRenderingOpenGL-6.2.so)

QT4_WRAP_CPP (project_HEADERS_MOC   viewer.h)
QT4_WRAP_CPP (project_HEADERS_MOC   connector.h)
QT4_WRAP_UI  (project_FORMS_HEADERS ${project_FORMS})

INCLUDE         (${QT_USE_FILE} )
ADD_DEFINITIONS (${QT_DEFINITIONS})

ADD_EXECUTABLE  (pcl_visualizer ${project_SOURCES}
                                ${project_FORMS_HEADERS}
                                ${project_HEADERS_MOC})

TARGET_LINK_LIBRARIES (pcl_visualizer ${QT_LIBRARIES} ${PCL_LIBRARIES} )


