# --------------------------------------------------------
#  Copyright (C) 2004-2021 by EMGU Corporation. All rights reserved.
# --------------------------------------------------------

IF(EMGU_CV_BUILD OR EMGU_CV_EXAMPLE_BUILD)
  IF (DOTNET_FOUND AND NOT (HAVE_IOS_ONLY))
    #IF(WIN32 AND (MSVC_VERSION GREATER 1900)) #need MSVC to be at least 2017
    PROJECT(Emgu.CV.Models.NetStandard)
    SET(EXTRA_MSBUILD_FLAGS "")
    IF(WIN32)
      SET(EXTRA_BUILD_FLAGS "/p:Platform=\"Any CPU\"")
    ENDIF()
    BUILD_CSPROJ_IN_SOLUTION(${PROJECT_NAME} "${CMAKE_CURRENT_SOURCE_DIR}/../../Solution/CrossPlatform/Emgu.CV.sln" "Emgu.CV.Models.NetStandard" "${EXTRA_BUILD_FLAGS}" ALL)

    INSTALL(
      FILES 
      ${CMAKE_CURRENT_SOURCE_DIR}/../../libs/Emgu.CV.Models.xml
      ${CMAKE_CURRENT_SOURCE_DIR}/../../libs/Emgu.CV.Models.dll 
      DESTINATION ${CPACK_PACKAGE_CLI_FOLDER}
      COMPONENT emgucv_binary)	  

    ADD_DEPENDENCIES(${PROJECT_NAME} Emgu.CV.Platform.NetStandard)  
    
    INSTALL(
      DIRECTORY
      ${CMAKE_CURRENT_SOURCE_DIR}
      DESTINATION .
      COMPONENT emgucv_source
      FILES_MATCHING 
      PATTERN "Emgu.CV.Models.NetStandard.csproj"
	  PATTERN "*.cs"
      PATTERN ".svn" EXCLUDE
      PATTERN "obj" EXCLUDE
      PATTERN "CMakeFiles" EXCLUDE
      PATTERN "${PROJECT_NAME}.dir" EXCLUDE
      )
    if(ENABLE_SOLUTION_FOLDERS)
      set_target_properties(${PROJECT_NAME} PROPERTIES FOLDER "emgu")
	endif() 
  ENDIF()
ENDIF()
