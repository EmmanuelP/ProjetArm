examples = [
  ['example1', ['example1.s']],
  ['example2', ['example2.s']],
  ['example3', ['example2.s']],
  ['example4', ['example4.s']],
  ['insertion_sort', ['insertion_sort.c']]
]

foreach example: examples
  executable(
    example[0],
    example[1],
    c_args:['-mbig-endian'],
    link_args: [
      '-nostdlib', '-T', join_paths(meson.current_source_dir(), 'linker_script'),
      '-n', '--entry', 'main', '-Wl,-EB'
    ]
  )
endforeach
