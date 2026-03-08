cmake_minimum_required(VERSION 3.20.0)

# MacOS build reference
# https://github.com/microsoft/vcpkg/blob/2626652f01caffa87a42f354d6fc43552ebd8db2/ports/irrlicht/CMakeLists.txt

project(irrlicht LANGUAGES C CXX)

file(GLOB SRC_FILES
    "include/*.h"
    "source/Irrlicht/*.cpp"
    "source/Irrlicht/zlib/zlib.h"
    "source/Irrlicht/zlib/adler32.c"
    "source/Irrlicht/zlib/compress.c"
    "source/Irrlicht/zlib/crc32.h"
    "source/Irrlicht/zlib/crc32.c"
    "source/Irrlicht/zlib/deflate.h"
    "source/Irrlicht/zlib/deflate.c"
    "source/Irrlicht/zlib/inffast.h"
    "source/Irrlicht/zlib/inffast.c"
    "source/Irrlicht/zlib/inflate.h"
    "source/Irrlicht/zlib/inflate.c"
    "source/Irrlicht/zlib/inftrees.h"
    "source/Irrlicht/zlib/inftrees.c"
    "source/Irrlicht/zlib/trees.h"
    "source/Irrlicht/zlib/trees.c"
    "source/Irrlicht/zlib/uncompr.c"
    "source/Irrlicht/zlib/zutil.h"
    "source/Irrlicht/zlib/zutil.c"
    "source/Irrlicht/jpeglib/jaricom.c"
    "source/Irrlicht/jpeglib/jcapimin.c"
    "source/Irrlicht/jpeglib/jcapistd.c"
    "source/Irrlicht/jpeglib/jcarith.c"
    "source/Irrlicht/jpeglib/jccoefct.c"
    "source/Irrlicht/jpeglib/jccolor.c"
    "source/Irrlicht/jpeglib/jcdctmgr.c"
    "source/Irrlicht/jpeglib/jchuff.c"
    "source/Irrlicht/jpeglib/jcinit.c"
    "source/Irrlicht/jpeglib/jcmainct.c"
    "source/Irrlicht/jpeglib/jcmarker.c"
    "source/Irrlicht/jpeglib/jcmaster.c"
    "source/Irrlicht/jpeglib/jcomapi.c"
    "source/Irrlicht/jpeglib/jcparam.c"
    "source/Irrlicht/jpeglib/jcprepct.c"
    "source/Irrlicht/jpeglib/jcsample.c"
    "source/Irrlicht/jpeglib/jctrans.c"
    "source/Irrlicht/jpeglib/jdapimin.c"
    "source/Irrlicht/jpeglib/jdapistd.c"
    "source/Irrlicht/jpeglib/jdarith.c"
    "source/Irrlicht/jpeglib/jdatadst.c"
    "source/Irrlicht/jpeglib/jdatasrc.c"
    "source/Irrlicht/jpeglib/jdcoefct.c"
    "source/Irrlicht/jpeglib/jdcolor.c"
    "source/Irrlicht/jpeglib/jddctmgr.c"
    "source/Irrlicht/jpeglib/jdhuff.c"
    "source/Irrlicht/jpeglib/jdinput.c"
    "source/Irrlicht/jpeglib/jdmainct.c"
    "source/Irrlicht/jpeglib/jdmarker.c"
    "source/Irrlicht/jpeglib/jdmaster.c"
    "source/Irrlicht/jpeglib/jdmerge.c"
    "source/Irrlicht/jpeglib/jdpostct.c"
    "source/Irrlicht/jpeglib/jdsample.c"
    "source/Irrlicht/jpeglib/jdtrans.c"
    "source/Irrlicht/jpeglib/jerror.c"
    "source/Irrlicht/jpeglib/jfdctflt.c"
    "source/Irrlicht/jpeglib/jfdctfst.c"
    "source/Irrlicht/jpeglib/jfdctint.c"
    "source/Irrlicht/jpeglib/jidctflt.c"
    "source/Irrlicht/jpeglib/jidctfst.c"
    "source/Irrlicht/jpeglib/jidctint.c"
    "source/Irrlicht/jpeglib/jmemmgr.c"
    "source/Irrlicht/jpeglib/jmemnobs.c"
    "source/Irrlicht/jpeglib/jquant1.c"
    "source/Irrlicht/jpeglib/jquant2.c"
    "source/Irrlicht/jpeglib/jutils.c"
    "source/Irrlicht/libpng/png.c"
    "source/Irrlicht/libpng/pngerror.c"
    "source/Irrlicht/libpng/pngget.c"
    "source/Irrlicht/libpng/pngmem.c"
    "source/Irrlicht/libpng/pngpread.c"
    "source/Irrlicht/libpng/pngread.c"
    "source/Irrlicht/libpng/pngrio.c"
    "source/Irrlicht/libpng/pngrtran.c"
    "source/Irrlicht/libpng/pngrutil.c"
    "source/Irrlicht/libpng/pngset.c"
    "source/Irrlicht/libpng/pngtrans.c"
    "source/Irrlicht/libpng/pngwio.c"
    "source/Irrlicht/libpng/pngwrite.c"
    "source/Irrlicht/libpng/pngwtran.c"
    "source/Irrlicht/libpng/pngwutil.c"
    "source/Irrlicht/libpng/intel/intel_init.c"
    "source/Irrlicht/libpng/intel/filter_sse2_intrinsics.c"
)

if (APPLE)
    file(GLOB IRR_SRC_FILES_MACOS "source/Irrlicht/MacOSX/*.mm" "source/Irrlicht/MacOSX/*.h" )
    set(SRC_FILES ${SRC_FILES} ${IRR_SRC_FILES_MACOS})
endif()

add_library(${PROJECT_NAME} STATIC ${SRC_FILES})

target_include_directories(${PROJECT_NAME}
    PUBLIC
        "${CMAKE_CURRENT_SOURCE_DIR}/include"
    PRIVATE
        "${CMAKE_CURRENT_SOURCE_DIR}/source/Irrlicht"
        "${CMAKE_CURRENT_SOURCE_DIR}/source/Irrlicht/jpeglib"
        "${CMAKE_CURRENT_SOURCE_DIR}/source/Irrlicht/libpng"
        "${CMAKE_CURRENT_SOURCE_DIR}/source/Irrlicht/zlib"
)

target_compile_definitions(${PROJECT_NAME} PUBLIC
    _IRR_STATIC_LIB_
    NO_IRR_USE_NON_SYSTEM_BZLIB_
    NO_IRR_COMPILE_WITH_BZIP2_
    NO_IRR_COMPILE_WITH_LZMA_
    NO_IRR_COMPILE_WITH_CONSOLE_DEVICE_
    NO_IRR_COMPILE_WITH_DIRECT3D_8_
    NO_IRR_COMPILE_WITH_DIRECTINPUT_JOYSTICK_
    NO_IRR_COMPILE_WITH_SOFTWARE_
    NO_IRR_COMPILE_WITH_BURNINGSVIDEO_
    NO_IRR_COMPILE_WITH_IRR_SCENE_LOADER_
    NO_IRR_COMPILE_WITH_SKINNED_MESH_SUPPORT_
    NO_IRR_COMPILE_WITH_IRR_MESH_LOADER_
    NO_IRR_COMPILE_WITH_HALFLIFE_LOADER_
    NO_IRR_COMPILE_WITH_MD2_LOADER_
    NO_IRR_COMPILE_WITH_MD3_LOADER_
    NO_IRR_COMPILE_WITH_3DS_LOADER_
    NO_IRR_COMPILE_WITH_COLLADA_LOADER_
    NO_IRR_COMPILE_WITH_CSM_LOADER_
    NO_IRR_COMPILE_WITH_BSP_LOADER_
    NO_IRR_COMPILE_WITH_DMF_LOADER_
    NO_IRR_COMPILE_WITH_LMTS_LOADER_
    NO_IRR_COMPILE_WITH_MY3D_LOADER_
    NO_IRR_COMPILE_WITH_OBJ_LOADER_
    NO_IRR_COMPILE_WITH_OCT_LOADER_
    NO_IRR_COMPILE_WITH_LWO_LOADER_
    NO_IRR_COMPILE_WITH_STL_LOADER_
    NO_IRR_COMPILE_WITH_PLY_LOADER_
    NO_IRR_COMPILE_WITH_SMF_LOADER_
    NO_IRR_COMPILE_WITH_IRR_WRITER_
    NO_IRR_COMPILE_WITH_COLLADA_WRITER_
    NO_IRR_COMPILE_WITH_STL_WRITER_
    NO_IRR_COMPILE_WITH_OBJ_WRITER_
    NO_IRR_COMPILE_WITH_PLY_WRITER_
    NO_IRR_COMPILE_WITH_PCX_LOADER_
    NO_IRR_COMPILE_WITH_PPM_LOADER_
    NO_IRR_COMPILE_WITH_PSD_LOADER_
    NO_IRR_COMPILE_WITH_TGA_LOADER_
    NO_IRR_COMPILE_WITH_WAL_LOADER_
    NO_IRR_COMPILE_WITH_LMP_LOADER_
    NO_IRR_COMPILE_WITH_RGB_LOADER_
    NO_IRR_COMPILE_WITH_PCX_WRITER_
    NO_IRR_COMPILE_WITH_PPM_WRITER_
    NO_IRR_COMPILE_WITH_PSD_WRITER_
    NO_IRR_COMPILE_WITH_TGA_WRITER_
    NO__IRR_COMPILE_WITH_PAK_ARCHIVE_LOADER_
    NO__IRR_COMPILE_WITH_NPK_ARCHIVE_LOADER_
    NO__IRR_COMPILE_WITH_WAD_ARCHIVE_LOADER_
    NO_IRR_COMPILE_WITH_ZIP_ENCRYPTION_
    PNG_INTEL_SSE
    PNG_ARM_NEON_OPT=0
    PNG_ARM_NEON_IMPLEMENTATION=0
)

if(MSVC)
    target_compile_options(${PROJECT_NAME} PRIVATE
        /GR-           
        /EHs-c-        
        /D_HAS_EXCEPTIONS=0 
    )
    target_compile_definitions(${PROJECT_NAME} PRIVATE 
        UNICODE
        _UNICODE
        _IRR_WCHAR_FILESYSTEM
        NO_IRR_COMPILE_WITH_DIRECT3D_9_
        NO_IRR_COMPILE_WITH_JOYSTICK_EVENTS_
    )
else()
    target_compile_options(${PROJECT_NAME} PRIVATE    
        -fno-rtti
        -fno-exceptions 
    )
    if (APPLE)
        target_compile_definitions(${PROJECT_NAME} PRIVATE GL_SILENCE_DEPRECATION)
        target_include_directories(${PROJECT_NAME} PRIVATE source/Irrlicht/MacOSX)
        target_compile_definitions(${PROJECT_NAME} PRIVATE SYSTEM=MacOSX)

        target_link_libraries(${PROJECT_NAME} ${OSX_LIBRARIES})

        target_compile_options(${PROJECT_NAME} PRIVATE "-ObjC++")

        set(ADDITIONAL_LIRARIES
            "-framework OpenGL"
            "-framework IOKit"
            "-framework Carbon"
            "-framework AppKit"
            "-framework Cocoa")
    else ()
        target_compile_definitions(${PROJECT_NAME} PRIVATE "NO_IRR_COMPILE_WITH_JOYSTICK_EVENTS_")
    endif ()
endif()