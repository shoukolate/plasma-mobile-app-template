set(%{APPNAMELC}_SRCS
    main.cpp
    )

qt5_add_resources(RESOURCES resources.qrc)
add_executable(%{APPNAMELC} ${%{APPNAMELC}_SRCS} ${RESOURCES})
target_link_libraries(%{APPNAMELC} Qt5::Core Qt5::Qml Qt5::Quick Qt5::Svg)
install(TARGETS %{APPNAMELC} ${KF5_INSTALL_TARGETS_DEFAULT_ARGS})
