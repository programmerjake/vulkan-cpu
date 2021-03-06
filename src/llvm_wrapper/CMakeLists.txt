# Copyright 2017 Jacob Lifshay
#
# Permission is hereby granted, free of charge, to any person obtaining a copy
# of this software and associated documentation files (the "Software"), to deal
# in the Software without restriction, including without limitation the rights
# to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
# copies of the Software, and to permit persons to whom the Software is
# furnished to do so, subject to the following conditions:
#
# The above copyright notice and this permission notice shall be included in all
# copies or substantial portions of the Software.
#
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
# IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
# FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
# AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
# LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
# OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
# SOFTWARE.
#
cmake_minimum_required(VERSION 3.3 FATAL_ERROR)

set(sources llvm_wrapper.cpp
            orc_compile_stack.cpp)
add_library(kazan_llvm_wrapper STATIC ${sources})
if(0)
llvm_map_components_to_libnames(llvm_libraries core native analysis orcjit mcjit nativecodegen ipo scalaropts vectorize)
else()
set(llvm_libraries LLVM)
endif()
target_link_libraries(kazan_llvm_wrapper util ${llvm_libraries})
set_source_files_properties(orc_compile_stack.cpp PROPERTIES COMPILE_FLAGS -fno-rtti) # prevent link errors with missing type info
