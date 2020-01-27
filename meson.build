project('vlc-wl-idle-inhibit', 'c',
  version: '0.1')

vlc_deps = dependency('vlc-plugin', version: '>= 3.0.8')

library('vlc_wl-idle-inhibit',
  'wl-idle-inhibit.c',
  dependencies: [vlc_deps],
  cpp_args: '-DMODULE_STRING="wl-idle-inhibit"')
