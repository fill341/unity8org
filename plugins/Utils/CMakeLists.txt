include_directories(
    ${CMAKE_CURRENT_SOURCE_DIR}
    ${CMAKE_CURRENT_BINARY_DIR}
)

include_directories(
    SYSTEM
    ${Qt5Gui_PRIVATE_INCLUDE_DIRS}
    ${Qt5Quick_PRIVATE_INCLUDE_DIRS}
    ${GIO_INCLUDE_DIRS}
)

set(QMLPLUGIN_SRC
    activefocuslogger.cpp
    ${APPLICATION_API_INCLUDEDIR}/unity/shell/application/ApplicationManagerInterface.h
    ${APPLICATION_API_INCLUDEDIR}/unity/shell/application/ApplicationInfoInterface.h
    applicationsfiltermodel.cpp
    ${LAUNCHER_API_INCLUDEDIR}/unity/shell/launcher/AppDrawerModelInterface.h
    ${LAUNCHER_API_INCLUDEDIR}/unity/shell/launcher/LauncherItemInterface.h
    ${LAUNCHER_API_INCLUDEDIR}/unity/shell/launcher/LauncherModelInterface.h
    appdrawerproxymodel.cpp
    constants.cpp
    WindowInputMonitor.cpp
    inputwatcher.cpp
    qlimitproxymodelqml.cpp
    unitysortfilterproxymodelqml.cpp
    Timer.cpp
    unitymenumodelpaths.cpp
    windowinputfilter.cpp
    easingcurve.cpp
    windowstatestorage.cpp
    timezoneFormatter.cpp
    inputeventgenerator.cpp
    deviceconfigparser.cpp
    globalfunctions.cpp
    URLDispatcher.cpp
    tabfocusfence.cpp
    expressionfiltermodel.cpp
    quicklistproxymodel.cpp
    plugin.cpp
    )

add_library(Utils-qml SHARED
    ${QMLPLUGIN_SRC}
    )

target_link_libraries(Utils-qml ${GIO_LDFLAGS})

# Because this is an internal support library, we want
# to expose all symbols in it. Consider changing this
# either to a static library or just using the
# files directly in targets.
set_target_properties(Utils-qml PROPERTIES COMPILE_FLAGS -fvisibility=default)

qt5_use_modules(Utils-qml Qml Quick DBus Network Gui Sql Concurrent)

add_unity8_plugin(Utils 0.1 Utils TARGETS Utils-qml)
