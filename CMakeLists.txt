cmake_minimum_required(VERSION 3.28)

project(ex-vi DESCRIPTION "BSD ex-vi" LANGUAGES C)

set(CMAKE_C_STANDARD 99)

# add_subdirectory(libterm)

# Features
set(FEATURES -DLISPCODE -DCHDIR -DFASTTAG -DUCVISUAL -DBIT8)
set(TERMLIB ncurses)
set(MALLOC src/mapmalloc.c)

# Set sources files
set(SOURCES
    src/ex.c
    src/ex_addr.c
    src/ex_cmds.c
    src/ex_cmds2.c
    src/ex_cmdsub.c
    src/ex_data.c
    src/ex_extern.c
    src/ex_get.c 
    src/ex_io.c 
    src/ex_put.c
    src/ex_re.c
    src/ex_set.c
    src/ex_subr.c 
    src/ex_tagio.c 
    src/ex_temp.c 
    src/ex_tty.c 
    src/ex_unix.c
    src/ex_v.c
    src/ex_vadj.c
    src/ex_vget.c
    src/ex_vmain.c
    src/ex_voper.c
    src/ex_vops.c
    src/ex_vops2.c
    src/ex_vops3.c
    src/ex_vput.c
    src/ex_vwind.c
    src/printf.c
    src/ex_version.c)

add_custom_command(OUTPUT src/ex_vars.h
                   COMMAND sh makeoptions ${FEATURES}
                   WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR})
add_custom_target(run_code_generation DEPENDS src/ex_vars.h)

add_executable(ex)

target_sources(ex PRIVATE ${SOURCES} ${MALLOC})
add_dependencies(ex run_code_generation)

target_include_directories(ex PRIVATE .)
target_compile_definitions(ex PRIVATE ${FEATURES} -DVMUNIX -DLARGEF)

target_link_libraries(ex PRIVATE ${TERMLIB})