
function (target_clang_libraries target)
  find_package(LLVM 4.0 REQUIRED CONFIG)

  get_filename_component(PARENT_DIR ${LLVM_INCLUDE_DIRS} DIRECTORY)
  set(LLVM_LIB_DIR ${PARENT_DIR}/lib)

  foreach(component ${ARGN})
    unset(LIB_PATH CACHE)
    find_library(LIB_PATH ${component} PATHS "${LLVM_LIB_DIR}" NO_DEFAULT_PATH)
    target_link_libraries(${target} ${LIB_PATH})
  endforeach()
endfunction ()

function (target_llvm_libraries target)
  find_package(LLVM 4.0 REQUIRED CONFIG)

  llvm_map_components_to_libnames(llvm_libs
    ${ARGN}
  )

  #target_link_libraries(${target}
  #  ${llvm_libs}
  #)

  ## workaround for now
  target_link_libraries(${target}
    LLVM-4.0
  )

  target_include_directories(${target} PUBLIC
    ${LLVM_INCLUDE_DIRS}
  )
  target_compile_definitions(${target} PUBLIC
    ${LLVM_DEFINITIONS}
  )

endfunction()
