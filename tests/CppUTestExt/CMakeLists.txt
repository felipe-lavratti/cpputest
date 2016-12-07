set(CppUTestExtTests_src
    AllTests.cpp
    CodeMemoryReporterTest.cpp
    GMockTest.cpp
    GTest1Test.cpp
    MemoryReportAllocatorTest.cpp
    MemoryReporterPluginTest.cpp
    MemoryReportFormatterTest.cpp
    MockActualCallTest.cpp
    MockCheatSheetTest.cpp
    MockCallTest.cpp
    MockComparatorCopierTest.cpp
    MockExpectedCallTest.cpp
    ExpectedFunctionsListTest.cpp
    MockFailureReporterForTest.cpp
    MockFailureTest.cpp
    MockHierarchyTest.cpp
    MockNamedValueTest.cpp
    MockParameterTest.cpp
    MockPluginTest.cpp
    MockSupportTest.cpp
    MockSupport_cTestCFile.c
    MockSupport_cTest.cpp
    MockStrictOrderTest.cpp
    MockReturnValueTest.cpp
    OrderedTestTest.cpp
)


# Mac OS X doesn't support IEEE754
IF(NOT ${CMAKE_SYSTEM_NAME} MATCHES "Darwin")
   list(APPEND CppUTestExtTests_src IEEE754PluginTest.cpp
                                    IEEE754PluginTest_c.c
       )
ENDIF(NOT ${CMAKE_SYSTEM_NAME} MATCHES "Darwin")

if (MINGW)
    find_package (Threads REQUIRED)
    set(THREAD_LIB "pthread")
endif (MINGW)

add_executable(CppUTestExtTests ${CppUTestExtTests_src})
cpputest_normalize_test_output_location(CppUTestExtTests)
target_link_libraries(CppUTestExtTests CppUTest CppUTestExt ${THREAD_LIB} ${CPPUNIT_EXTERNAL_LIBRARIES})
cpputest_buildtime_discover_tests(CppUTestExtTests)
