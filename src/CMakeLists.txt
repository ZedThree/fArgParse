set(CMAKE_Fortran_MODULE_DIRECTORY ${FARGPARSE_BINARY_DIR}/mod)

set(srcs
  AbstractArgParser.F90
  BaseAction.F90
  HelpAction.F90
  StoreAction.F90
  StoreConstAction.F90
  StoreTrueAction.F90
  StoreFalseAction.F90
  ActionVector.F90
  String.F90
  StringActionMap.F90

  ArgParser.F90
  Cast.F90
  CommandLineArguments.F90
  ErrorCodes.F90
  KeywordEnforcer.F90
  None.F90

  # The package
  fArgParse.F90
  )

set (dest "FARGPARSE-${FARGPARSE_VERSION_MAJOR}.${FARGPARSE_VERSION_MINOR}")

add_library(fargparse STATIC ${srcs})
target_include_directories (fargparse PUBLIC
  $<BUILD_INTERFACE:${FARGPARSE_BINARY_DIR}/mod>
  $<INSTALL_INTERFACE:${dest}/include>
  )
target_include_directories (fargparse PRIVATE ${FARGPARSE_SOURCE_DIR}/include)
target_link_libraries(fargparse external-fargparse)


install (DIRECTORY ${FARGPARSE_BINARY_DIR}/mod/ DESTINATION ${dest}/include)
install (TARGETS fargparse EXPORT FARGPARSE DESTINATION "${dest}/lib")
install (EXPORT FARGPARSE DESTINATION "${dest}/cmake")
