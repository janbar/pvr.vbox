project(pvr.vbox)

cmake_minimum_required(VERSION 2.6)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${PROJECT_SOURCE_DIR})

enable_language(CXX)

find_package(kodi REQUIRED)
find_package(kodiplatform REQUIRED)
find_package(p8-platform REQUIRED)

include_directories(${kodiplatform_INCLUDE_DIRS}
                    ${p8-platform_INCLUDE_DIRS}
                    ${KODI_INCLUDE_DIR}
                    ${PROJECT_SOURCE_DIR})

# Sources and headers
set(VBOX_SOURCES 
                src/client.h
                src/client.cpp
                src/compat.h)

set(VBOX_SOURCES_VBOX
                src/vbox/Channel.h
                src/vbox/ChannelStreamingStatus.h
                src/vbox/ChannelStreamingStatus.cpp
                src/vbox/ContentIdentifier.h
                src/vbox/Exceptions.h
                src/vbox/GuideChannelMapper.h
                src/vbox/GuideChannelMapper.cpp
                src/vbox/Recording.h
                src/vbox/Recording.cpp
                src/vbox/Settings.h
                src/vbox/SoftwareVersion.h
                src/vbox/SoftwareVersion.cpp
                src/vbox/StartupStateHandler.h
                src/vbox/StartupStateHandler.cpp
                src/vbox/Utilities.h
                src/vbox/VBox.h
                src/vbox/VBox.cpp)
                      
set(VBOX_SOURCES_VBOX_REQUEST 
                src/vbox/request/ApiRequest.h
                src/vbox/request/ApiRequest.cpp
                src/vbox/request/FileRequest.h
                src/vbox/request/Request.h)
                 
set(VBOX_SOURCES_VBOX_RESPONSE
                src/vbox/response/Content.h
                src/vbox/response/Content.cpp
                src/vbox/response/Factory.h
                src/vbox/response/Response.h
                src/vbox/response/Response.cpp)

set(VBOX_SOURCES_TIMESHIFT 
                src/timeshift/Buffer.h
                src/timeshift/Buffer.cpp
                src/timeshift/DummyBuffer.h
                src/timeshift/FilesystemBuffer.h
                src/timeshift/FilesystemBuffer.cpp)
                
set(VBOX_SOURCES_XMLTV 
                src/xmltv/Channel.h
                src/xmltv/Channel.cpp
                src/xmltv/Guide.h
                src/xmltv/Guide.cpp
                src/xmltv/Programme.h
                src/xmltv/Programme.cpp
                src/xmltv/Schedule.h
                src/xmltv/Schedule.cpp
                src/xmltv/Utilities.h
                src/xmltv/Utilities.cpp)

source_group("Source Files" FILES ${VBOX_SOURCES})
source_group("Source Files\\vbox" FILES ${VBOX_SOURCES_VBOX})
source_group("Source Files\\vbox\\request" FILES ${VBOX_SOURCES_VBOX_REQUEST})
source_group("Source Files\\vbox\\response" FILES ${VBOX_SOURCES_VBOX_RESPONSE})
source_group("Source Files\\timeshift" FILES ${VBOX_SOURCES_TIMESHIFT})
source_group("Source Files\\xmltv" FILES ${VBOX_SOURCES_XMLTV})

# Library files
set(VBOX_LIBRARIES_TINYXML2
                lib/tinyxml2/tinyxml2.h
                lib/tinyxml2/tinyxml2.cpp)

source_group("Library Files\\tinyxml2" FILES ${VBOX_LIBRARIES_TINYXML2})
                 
# Resource files
set(VBOX_RESOURCES 
                README.md
                pvr.vbox/addon.xml
                pvr.vbox/changelog.txt
                pvr.vbox/icon.png
                pvr.vbox/resources/settings.xml
                pvr.vbox/resources/language/resource.language.en_gb/strings.po)

source_group("Resource Files" FILES ${VBOX_RESOURCES})

# Append our custom file definitions
list(APPEND VBOX_SOURCES 
                ${VBOX_SOURCES_VBOX} 
                ${VBOX_SOURCES_VBOX_REQUEST}
                ${VBOX_SOURCES_VBOX_RESPONSE}
                ${VBOX_SOURCES_TIMESHIFT}
                ${VBOX_SOURCES_XMLTV}
                ${VBOX_RESOURCES}
                ${VBOX_LIBRARIES_TINYXML2})

set(DEPLIBS ${p8-platform_LIBRARIES})
build_addon(pvr.vbox VBOX DEPLIBS)

include(CPack)
