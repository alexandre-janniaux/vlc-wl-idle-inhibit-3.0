project('vlc-wl-idle-inhibit', 'c',
  version: '0.1')

vlc_deps = dependency('vlc-plugin', version: '>= 3.0.8', required: true)

# Wayland dependencies
wayland_client = dependency('wayland-client', required: true)
wl_scanner = dependency('wayland-scanner', native: true, required: true)
prog_scanner = find_program(wl_scanner.get_pkgconfig_variable('wayland_scanner'))
protocols = dependency('wayland-protocols', required: true)

idle_path = protocols.get_pkgconfig_variable('pkgdatadir')
idle_headers = custom_target(
  'gen-client-header',
  command: [prog_scanner, 'client-header', '@INPUT@', '@OUTPUT@'],
  input: idle_path + '/unstable/idle-inhibit/idle-inhibit-unstable-v1.xml',
  output: 'idle-inhibit-client-protocol.h')
idle_sources = custom_target(
  'gen-private-code',
  command: [prog_scanner, 'private-code', '@INPUT@', '@OUTPUT@'],
  input: idle_path + '/unstable/idle-inhibit/idle-inhibit-unstable-v1.xml',
  output: 'idle-inhibit-client-protocol.c')

library('wl_idle_inhibit_plugin',
  ['wl-idle-inhibit.c', idle_headers, idle_sources],
  dependencies: [vlc_deps, wayland_client],
  c_args: '-DMODULE_STRING="wl-idle-inhibit"',
  install_dir: '/usr/lib/vlc/plugins/misc/',
  install: true, )
