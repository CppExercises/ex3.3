# Exercise EX3.3

This exercise is part **three** of three parts of EX3. See also [Item 000](https://cppitems.github.io/#/item/000) for an overview and deadlines. The submission deadline for EX3 (all three parts) is **Mo 10.01.2021, 4pm**. The sources related to EX3.3 are available at https://github.com/cppitems/ex3.3.

## Running Result

```bash
wang@wang-virtual-machine:~/Documents/ex3.3/build$ cmake -DBUILD_BENCHMARK=ON -DCMAKE_BUILD_TYPE=Release ..
-- -----> Current build type set to: Release
-- -----> thread sanitizer is only turned on for the build type: Debug
-- Building header-only library
-- Configuring done
-- Generating done
-- Build files have been written to: /home/wang/Documents/ex3.3/build
```

```bash
wang@wang-virtual-machine:~/Documents/ex3.3/build$ make
Scanning dependencies of target sync_benchmark
[ 10%] Building CXX object CMakeFiles/sync_benchmark.dir/src/sync_benchmark.cpp.o
[ 20%] Linking CXX executable sync_benchmark
[ 20%] Built target sync_benchmark
Scanning dependencies of target TestA_SMF_and_get
[ 30%] Building CXX object tests/CMakeFiles/TestA_SMF_and_get.dir/TestA_SMF_and_get.cpp.o
In file included from /home/wang/Documents/ex3.3/tests/TestA_SMF_and_get.cpp:2:0:
/home/wang/Documents/ex3.3/include/shared_ptr.hpp:16:56: note: #pragma message: SYNC_METHOD == SYNC_CRITICAL_SECTIONS
 #pragma message("SYNC_METHOD == SYNC_CRITICAL_SECTIONS")
                                                        ^
[ 40%] Linking CXX executable TestA_SMF_and_get
[ 40%] Built target TestA_SMF_and_get
Scanning dependencies of target TestC_compare
[ 50%] Building CXX object tests/CMakeFiles/TestC_compare.dir/TestC_compare.cpp.o
In file included from /home/wang/Documents/ex3.3/tests/TestC_compare.cpp:2:0:
/home/wang/Documents/ex3.3/include/shared_ptr.hpp:16:56: note: #pragma message: SYNC_METHOD == SYNC_CRITICAL_SECTIONS
 #pragma message("SYNC_METHOD == SYNC_CRITICAL_SECTIONS")
                                                        ^
[ 60%] Linking CXX executable TestC_compare
[ 60%] Built target TestC_compare
Scanning dependencies of target TestD_threads
[ 70%] Building CXX object tests/CMakeFiles/TestD_threads.dir/TestD_threads.cpp.o
In file included from /home/wang/Documents/ex3.3/tests/TestD_threads.cpp:3:0:
/home/wang/Documents/ex3.3/include/shared_ptr.hpp:16:56: note: #pragma message: SYNC_METHOD == SYNC_CRITICAL_SECTIONS
 #pragma message("SYNC_METHOD == SYNC_CRITICAL_SECTIONS")
                                                        ^
[ 80%] Linking CXX executable TestD_threads
[ 80%] Built target TestD_threads
Scanning dependencies of target TestB_assign_reset
[ 90%] Building CXX object tests/CMakeFiles/TestB_assign_reset.dir/TestB_assign_reset.cpp.o
In file included from /home/wang/Documents/ex3.3/tests/TestB_assign_reset.cpp:1:0:
/home/wang/Documents/ex3.3/include/shared_ptr.hpp:16:56: note: #pragma message: SYNC_METHOD == SYNC_CRITICAL_SECTIONS
 #pragma message("SYNC_METHOD == SYNC_CRITICAL_SECTIONS")
                                                        ^
[100%] Linking CXX executable TestB_assign_reset
[100%] Built target TestB_assign_reset
wang@wang-virtual-machine:~/Documents/ex3.3/build$ ./sync_benchmark 
count = 400000 (expected count == 400000)
Benchmark using SYNC_ATOMICS:                      0.0131189 s
count = 400000 (expected count == 400000)
Benchmark using SYNC_CRITICAL_SECTIONS:            0.0327445 s
```

```bash
wang@wang-virtual-machine:~/Documents/ex3.3/build$ cmake -D CMAKE_BUILD_TYPE=Debug -D SYNC_METHOD=SYNC_CRITICAL_SECTIONS ..
-- -----> Current build type set to: Debug
-- -----> Congratulations, you are using the thread sanitizer
-- Building header-only library
-- Configuring done
-- Generating done
-- Build files have been written to: /home/wang/Documents/ex3.3/build
wang@wang-virtual-machine:~/Documents/ex3.3/build$ make
[ 20%] Built target sync_benchmark
Scanning dependencies of target TestA_SMF_and_get
[ 30%] Building CXX object tests/CMakeFiles/TestA_SMF_and_get.dir/TestA_SMF_and_get.cpp.o
In file included from /home/wang/Documents/ex3.3/tests/TestA_SMF_and_get.cpp:2:0:
/home/wang/Documents/ex3.3/include/shared_ptr.hpp:16:56: note: #pragma message: SYNC_METHOD == SYNC_CRITICAL_SECTIONS
 #pragma message("SYNC_METHOD == SYNC_CRITICAL_SECTIONS")
                                                        ^
[ 40%] Linking CXX executable TestA_SMF_and_get
[ 40%] Built target TestA_SMF_and_get
Scanning dependencies of target TestC_compare
[ 50%] Building CXX object tests/CMakeFiles/TestC_compare.dir/TestC_compare.cpp.o
In file included from /home/wang/Documents/ex3.3/tests/TestC_compare.cpp:2:0:
/home/wang/Documents/ex3.3/include/shared_ptr.hpp:16:56: note: #pragma message: SYNC_METHOD == SYNC_CRITICAL_SECTIONS
 #pragma message("SYNC_METHOD == SYNC_CRITICAL_SECTIONS")
                                                        ^
[ 60%] Linking CXX executable TestC_compare
[ 60%] Built target TestC_compare
Scanning dependencies of target TestD_threads
[ 70%] Building CXX object tests/CMakeFiles/TestD_threads.dir/TestD_threads.cpp.o
In file included from /home/wang/Documents/ex3.3/tests/TestD_threads.cpp:3:0:
/home/wang/Documents/ex3.3/include/shared_ptr.hpp:16:56: note: #pragma message: SYNC_METHOD == SYNC_CRITICAL_SECTIONS
 #pragma message("SYNC_METHOD == SYNC_CRITICAL_SECTIONS")
                                                        ^
[ 80%] Linking CXX executable TestD_threads
[ 80%] Built target TestD_threads
Scanning dependencies of target TestB_assign_reset
[ 90%] Building CXX object tests/CMakeFiles/TestB_assign_reset.dir/TestB_assign_reset.cpp.o
In file included from /home/wang/Documents/ex3.3/tests/TestB_assign_reset.cpp:1:0:
/home/wang/Documents/ex3.3/include/shared_ptr.hpp:16:56: note: #pragma message: SYNC_METHOD == SYNC_CRITICAL_SECTIONS
 #pragma message("SYNC_METHOD == SYNC_CRITICAL_SECTIONS")
                                                        ^
[100%] Linking CXX executable TestB_assign_reset
[100%] Built target TestB_assign_reset
wang@wang-virtual-machine:~/Documents/ex3.3/build$ ctest --verbose
UpdateCTestConfiguration  from :/home/wang/Documents/ex3.3/build/DartConfiguration.tcl
UpdateCTestConfiguration  from :/home/wang/Documents/ex3.3/build/DartConfiguration.tcl
Test project /home/wang/Documents/ex3.3/build
Constructing a list of tests
Done constructing a list of tests
Updating test list for fixtures
Added 0 tests to meet fixture requirements
Checking test dependency graph...
Checking test dependency graph end
test 1
    Start 1: TestA_SMF_and_get

1: Test command: /home/wang/Documents/ex3.3/build/tests/TestA_SMF_and_get
1: Test timeout computed to be: 10000000
1/4 Test #1: TestA_SMF_and_get ................   Passed    0.01 sec
test 2
    Start 2: TestB_assign_reset

2: Test command: /home/wang/Documents/ex3.3/build/tests/TestB_assign_reset
2: Test timeout computed to be: 10000000
2/4 Test #2: TestB_assign_reset ...............   Passed    0.01 sec
test 3
    Start 3: TestC_compare

3: Test command: /home/wang/Documents/ex3.3/build/tests/TestC_compare
3: Test timeout computed to be: 10000000
3/4 Test #3: TestC_compare ....................   Passed    0.01 sec
test 4
    Start 4: TestD_threads

4: Test command: /home/wang/Documents/ex3.3/build/tests/TestD_threads
4: Test timeout computed to be: 10000000
4/4 Test #4: TestD_threads ....................   Passed    0.01 sec

100% tests passed, 0 tests failed out of 4

Total Test time (real) =   0.04 sec
```

```bash
wang@wang-virtual-machine:~/Documents/ex3.3/build$ cmake -D CMAKE_BUILD_TYPE=Debug -D SYNC_METHOD=SYNC_ATOMICS ..
-- -----> Current build type set to: Debug
-- -----> Congratulations, you are using the thread sanitizer
-- Building header-only library
-- Configuring done
-- Generating done
-- Build files have been written to: /home/wang/Documents/ex3.3/build
wang@wang-virtual-machine:~/Documents/ex3.3/build$ make
[ 10%] Building CXX object CMakeFiles/sync_benchmark.dir/src/sync_benchmark.cpp.o
[ 20%] Linking CXX executable sync_benchmark
[ 20%] Built target sync_benchmark
Scanning dependencies of target TestA_SMF_and_get
[ 30%] Building CXX object tests/CMakeFiles/TestA_SMF_and_get.dir/TestA_SMF_and_get.cpp.o
In file included from /home/wang/Documents/ex3.3/tests/TestA_SMF_and_get.cpp:2:0:
/home/wang/Documents/ex3.3/include/shared_ptr.hpp:12:46: note: #pragma message: SYNC_METHOD == SYNC_ATOMICS
 #pragma message("SYNC_METHOD == SYNC_ATOMICS")
                                              ^
[ 40%] Linking CXX executable TestA_SMF_and_get
[ 40%] Built target TestA_SMF_and_get
Scanning dependencies of target TestC_compare
[ 50%] Building CXX object tests/CMakeFiles/TestC_compare.dir/TestC_compare.cpp.o
In file included from /home/wang/Documents/ex3.3/tests/TestC_compare.cpp:2:0:
/home/wang/Documents/ex3.3/include/shared_ptr.hpp:12:46: note: #pragma message: SYNC_METHOD == SYNC_ATOMICS
 #pragma message("SYNC_METHOD == SYNC_ATOMICS")
                                              ^
[ 60%] Linking CXX executable TestC_compare
[ 60%] Built target TestC_compare
Scanning dependencies of target TestD_threads
[ 70%] Building CXX object tests/CMakeFiles/TestD_threads.dir/TestD_threads.cpp.o
In file included from /home/wang/Documents/ex3.3/tests/TestD_threads.cpp:3:0:
/home/wang/Documents/ex3.3/include/shared_ptr.hpp:12:46: note: #pragma message: SYNC_METHOD == SYNC_ATOMICS
 #pragma message("SYNC_METHOD == SYNC_ATOMICS")
                                              ^
[ 80%] Linking CXX executable TestD_threads
[ 80%] Built target TestD_threads
Scanning dependencies of target TestB_assign_reset
[ 90%] Building CXX object tests/CMakeFiles/TestB_assign_reset.dir/TestB_assign_reset.cpp.o
In file included from /home/wang/Documents/ex3.3/tests/TestB_assign_reset.cpp:1:0:
/home/wang/Documents/ex3.3/include/shared_ptr.hpp:12:46: note: #pragma message: SYNC_METHOD == SYNC_ATOMICS
 #pragma message("SYNC_METHOD == SYNC_ATOMICS")
                                              ^
[100%] Linking CXX executable TestB_assign_reset
[100%] Built target TestB_assign_reset
wang@wang-virtual-machine:~/Documents/ex3.3/build$ ctest --verbose
UpdateCTestConfiguration  from :/home/wang/Documents/ex3.3/build/DartConfiguration.tcl
UpdateCTestConfiguration  from :/home/wang/Documents/ex3.3/build/DartConfiguration.tcl
Test project /home/wang/Documents/ex3.3/build
Constructing a list of tests
Done constructing a list of tests
Updating test list for fixtures
Added 0 tests to meet fixture requirements
Checking test dependency graph...
Checking test dependency graph end
test 1
    Start 1: TestA_SMF_and_get

1: Test command: /home/wang/Documents/ex3.3/build/tests/TestA_SMF_and_get
1: Test timeout computed to be: 10000000
1/4 Test #1: TestA_SMF_and_get ................   Passed    0.01 sec
test 2
    Start 2: TestB_assign_reset

2: Test command: /home/wang/Documents/ex3.3/build/tests/TestB_assign_reset
2: Test timeout computed to be: 10000000
2/4 Test #2: TestB_assign_reset ...............   Passed    0.01 sec
test 3
    Start 3: TestC_compare

3: Test command: /home/wang/Documents/ex3.3/build/tests/TestC_compare
3: Test timeout computed to be: 10000000
3/4 Test #3: TestC_compare ....................   Passed    0.01 sec
test 4
    Start 4: TestD_threads

4: Test command: /home/wang/Documents/ex3.3/build/tests/TestD_threads
4: Test timeout computed to be: 10000000
4/4 Test #4: TestD_threads ....................   Passed    0.01 sec

100% tests passed, 0 tests failed out of 4

Total Test time (real) =   0.05 sec
```

## Task description
In this exercise you are provided with a working implementation of a `shared_ptr`. This implementation is simplified compared to the `shared_ptr` in the stdlib:
- no `weak_ptr` is present
- no relation/conversion from `unique_ptr`
- no custom deleter (and no support for array types)
- no thread-safe reference counting (this means also not all SMFs and members are thread safe) **-> It is your task ensure thread-safetyness in this exercise**

It is your task to adapt the provide implementation of `shared_ptr` to provide thread-safe reference counting (like the "original" from the stlib). You should enable this thread-safetyness "twice" via different synchronization mechanisms:
- **Task1**: adapt `include/shared_ptr_sync_atomics.hpp` to use atomics to ensure the required synchronization between threads.
- **Task2**: adapt `include/shared_ptr_critical_section.hpp` to use critical sections (locks) to ensure the required synchronization between threads.

**Note**: Beside the `namespace`-name, the three implementations in the handout `include/shared_ptr_sync_none.hpp`,  `include/shared_ptr_sync_atomics.hpp` , and `include/shared_ptr_critical_sections.hpp` are identical. **You should only adapt the latter two files**.

Prepare yourself for a discussion of your implementations.

### Task details and tests
Tests are provided for the implementation of the `shared_ptr`:
- **TestA_SMF_and_get**: tests all special member functions.
- **TestB_assign_reset**: tests reset(...) and assignment with involvement of `nullptr`.
- **TestC_compare**: tests comparison between two `shared_ptr`s and between a `shared_ptr` and `nullptr`.
- **TestD_threads**: uses `shared_ptr`s to share a resource between multiple threads.

The only test which is failing for the provided implementation is **TestD_threads**: *data races* (i.e., unsynchronized access to a memory location) are present which are detected by the *thread-sanitizer* during runtime.

To build and run the tests for each of the two implementations use one of the following commands:
```bash
#cmake -D CMAKE_BUILD_TYPE=Debug -D SYNC_METHOD=SYNC_NONE .. # tests implementation in include/shared_ptr_sync_none.hpp
cmake -D CMAKE_BUILD_TYPE=Debug -D SYNC_METHOD=SYNC_ATOMICS .. # tests implementation in include/shared_ptr_sync_atomics.hpp
cmake -D CMAKE_BUILD_TYPE=Debug -D SYNC_METHOD=SYNC_CRITICAL_SECTIONS .. # tests implementation in include/shared_ptr_critical_sections.hpp
make
ctest --verbose # run all tests with failure output interleaved
./tests/TestD_threads # run a single test manually
```
**Note**: if you do not provide a define for `SYNC_METHOD`, `SYNC_METHOD=SYNC_NONE` is used as default, i.e. the non-thread-safe baseline implementation in `include/shared_ptr_sync_none.hpp` is selected and tested.

## Benchmark 
The benchmark in `src/sync_benchmark.cpp` measures the runtime of a scenario where a resource is passed to four threads via a `shared_pointer` (similar to **TestD_threads**) and each thread makes "heavy use" of the `shared_ptr`s SMFs due to passing it to a nested function in a loop. Further the benchmark utilizes and compares the two versions of the `shared_ptr` you implemented:
- `include/shared_ptr_sync_atomics.hpp` which uses *atomics* to synchronize access to the reference counters.
- `include/shared_ptr_sync_critical_sections.hpp` which uses *critical sections* (locks) to synchronize access to the reference counters.
You can build and run the benchmark using the following commands:
```bash
cmake -DBUILD_BENCHMARK=ON -DCMAKE_BUILD_TYPE=Release ..
make
./sync_benchmark
```
Inspect the runtimes reported by the benchmark and prepare yourself to discuss if and why this matches your expectations.

## References
- `std::shared_ptr`: https://en.cppreference.com/w/cpp/memory/shared_ptr
- `std::atomic`: https://en.cppreference.com/w/cpp/atomic/atomic
- `std::memory_order`: https://en.cppreference.com/w/cpp/atomic/memory_order
- `std::mutex`: https://en.cppreference.com/w/cpp/thread/mutex
- `std::lock_guard`: https://en.cppreference.com/w/cpp/thread/lock_guard
