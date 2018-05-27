cmake_minimum_required(VERSION 3.4.3)
project(SimpleProject)

add_subdirectory(llvm)

add_executable(simple-tool tool.cpp)

target_link_libraries(simple-tool
  -Wl,--start-group
  stdc++
)

target_llvm_libraries(simple-tool
  option
  support
  core
)

target_clang_libraries(simple-tool
  clangStaticAnalyzerFrontend
  clangApplyReplacements
  clangStaticAnalyzerCheckers
  clangCodeGen
  clangTidyUtils
  clangAST
  clangFormat
  clangIncludeFixerPlugin
  clangLex
  clangEdit
  clangTidyMiscModule
  clangReorderFields
  clangTidyLLVMModule
  clangTidyGoogleModule
  clangIncludeFixer
  clangFrontendTool
  clangARCMigrate
  clangChangeNamespace
  clangParse
  clangASTMatchers
  clangTidyPerformanceModule
  clangQuery
  clangMove
  clangAnalysis
  clangBasic
  clangTidyModernizeModule
  clangFrontend
  clangTidyCppCoreGuidelinesModule
  clangTidy
  clangStaticAnalyzerCore
  clangRename
  clangTidyBoostModule
  clangDriver
  clangRewriteFrontend
  clangRewrite
  clangIndex
  clangDynamicASTMatchers
  clangTidyMPIModule
  clangTidyCERTModule
  clangToolingCore
  clangTidyReadabilityModule
  clangSema
  clangSerialization
  clangTooling
)

target_link_libraries(simple-tool
  -Wl,--end-group
)

set_target_properties(simple-tool PROPERTIES
    CXX_STANDARD 11
    CXX_STANDARD_REQUIRED ON
)
