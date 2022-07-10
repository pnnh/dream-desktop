cmake_minimum_required(VERSION 3.15)

project(dream-desktop VERSION 0.1 LANGUAGES CXX)

set(CMAKE_INCLUDE_CURRENT_DIR ON)

set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(Qt6 COMPONENTS Core Quick Gui QuickControls2 Sql REQUIRED)

include_directories(src/include)

set(PROJECT_SOURCES
        src/main.cpp
        src/md5.cc src/md5.h
        src/wasm/wasm.h
        src/sqlite/sqlite.cc src/sqlite/sqlite.h
        src/models/videoListModel.cc src/models/videoListModel.h
        src/models/sqliteModel.cc src/models/sqliteModel.h)

qt_add_executable(dream-desktop
        MANUAL_FINALIZATION
        ${PROJECT_SOURCES})

target_link_libraries(dream-desktop
        PRIVATE Qt6::Core Qt6::Gui Qt6::Quick Qt6::QuickControls2 Qt6::Sql)

qt_import_qml_plugins(dream-desktop)
qt_finalize_executable(dream-desktop)

qt_add_qml_module(dream-desktop
        URI QtEditor
        VERSION 1.0
        SOURCES
        src/include/mytype.h src/models/mytype.cc
        QML_FILES
        src/qrc/main.qml
        src/qrc/list_videos.qml
        src/qrc/App.qml
        src/qrc/FxScrollBar.qml
        src/qrc/TaskList.qml
        src/qrc/NavList.qml
        RESOURCES
        res/images/flag-fill.png)