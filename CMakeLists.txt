cmake_minimum_required(VERSION 3.5)

project(Kursovaya VERSION 0.1 LANGUAGES CXX)

set(CMAKE_INCLUDE_CURRENT_DIR ON)

set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# QtCreator supports the following variables for Android, which are identical to qmake Android variables.
# Check https://doc.qt.io/qt/deployment-android.html for more information.
# They need to be set before the find_package( ...) calls below.

#if(ANDROID)
#    set(ANDROID_PACKAGE_SOURCE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/android")
#    if (ANDROID_ABI STREQUAL "armeabi-v7a")
#        set(ANDROID_EXTRA_LIBS
#            ${CMAKE_CURRENT_SOURCE_DIR}/path/to/libcrypto.so
#            ${CMAKE_CURRENT_SOURCE_DIR}/path/to/libssl.so)
#    endif()
#endif()

find_package(QT NAMES Qt6 Qt5 COMPONENTS Widgets REQUIRED)
find_package(Qt${QT_VERSION_MAJOR} COMPONENTS Widgets REQUIRED)
find_package(Qt6Sql)

set(PROJECT_SOURCES
        main.cpp
        mainwindow.cpp
        mainwindow.h
        mainwindow.ui
        opiniojnform.h
        opiniojnform.cpp
        opiniojnform.ui
        menuform.h
        menuform.cpp
        menuform.ui
        appoitmentform.h
        appoitmentform.cpp
        appoitmentform.ui
        myappoitmentsform.h
        myappoitmentsform.cpp
        myappoitmentsform.ui
        addpatientform.h
        addpatientform.cpp
        addpatientform.ui
        adddoctorform.h
        adddoctorform.cpp
        adddoctorform.ui
        outpatient_card_form.h
        outpatient_card_form.cpp
        outpatient_card_form.ui
        settingsform.h
        settingsform.cpp
        settingsform.ui
        DataBaseConnector.h
)

if(${QT_VERSION_MAJOR} GREATER_EQUAL 6)
    qt_add_executable(Kursovaya
        MANUAL_FINALIZATION
        ${PROJECT_SOURCES}
    )
else()
    if(ANDROID)
        add_library(Kursovaya SHARED
            ${PROJECT_SOURCES}
        )
    else()
        add_executable(Kursovaya
            ${PROJECT_SOURCES}
        )
    endif()
endif()

target_link_libraries(Kursovaya PRIVATE Qt${QT_VERSION_MAJOR}::Widgets Qt6::Sql)

set_target_properties(Kursovaya PROPERTIES
    MACOSX_BUNDLE_GUI_IDENTIFIER my.example.com
    MACOSX_BUNDLE_BUNDLE_VERSION ${PROJECT_VERSION}
    MACOSX_BUNDLE_SHORT_VERSION_STRING ${PROJECT_VERSION_MAJOR}.${PROJECT_VERSION_MINOR}
)

if(QT_VERSION_MAJOR EQUAL 6)
    qt_finalize_executable(Kursovaya)
endif()
