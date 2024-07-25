
add_library(termlib STATIC
    termcap.c
    tgoto.c
    tputs.c)

target_compile_options(termlib PRIVATE -DCM_N -DCM_GT -DCM_B -DCM_D -DVMUNIX -DLARGEF)