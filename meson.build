project('arm_simulator', 'c')

cc=meson.get_compiler('c')

threads_dep=dependency('threads')

flex = find_program('flex', required: false)
bison = find_program('bison', required: false)

lgen = generator (flex,output : '@BASENAME@.yy.c',
arguments : ['-P', '@BASENAME@_yy', '-o', '@OUTPUT@', '@INPUT@'])

scanner_source=lgen.process('scanner.l')

sources=[
  'csapp.c',
  'debug.c',
  'gdb_protocol.c',
  'util.c',
  'trace.c',
  'memory.c',
  'registers.c',
  'arm.c',
  'arm_constants.c',
  'arm_core.c',
  'arm_exception.c',
  'arm_instruction.c',
  'arm_data_processing.c',
  'arm_load_store.c',
  'arm_branch_other.c',
  scanner_source
]

headers=[
  'scanner.h',
  'csapp.h',
  'debug.h',
  'gdb_protocol.h',
  'util.h',
  'trace.h',
  'trace_location.h',
  'no_trace_location.h',
  'memory.h',
  'registers.h',
  'arm.h',
  'arm_constants.h',
  'arm_core.h',
  'arm_exception.h',
  'arm_instruction.h',
  'arm_data_processing.h',
  'arm_load_store.h',
  'arm_branch_other.h'
]

arm_sim_lib=static_library('arm_simulator', sources, headers, dependencies:threads_dep, native:true)

apps = ['arm_simulator', 'send_irq', 'memory_test']

foreach app: apps
  executable(app, app+'.c', link_with:arm_sim_lib, dependencies:threads_dep, native:true)
endforeach

if meson.is_cross_build()
  subdir('Examples')
else
  message('Examples are built only if cross compilation is enabled')
endif
