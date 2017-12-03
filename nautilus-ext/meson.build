libnautilus_seahorse_sources = [
  'seahorse-nautilus.c',
  'seahorse-nautilus-module.c',
]

libnautilus_seahorse_dependencies = [
  glib,
  libnautilus_extension,
]

libnautilus_seahorse = library('nautilus-seahorse',
  libnautilus_seahorse_sources,
  dependencies: libnautilus_seahorse_dependencies,
  include_directories: config_h_dir,
  install: true,
  install_dir: nautilus_ext_dir,
)
