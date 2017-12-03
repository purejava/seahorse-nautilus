marshaller = gnome.genmarshal('seahorse-marshal',
  sources: 'seahorse-marshal.list',
  prefix: 'seahorse_marshal',
)

# Resources
resources = gnome.compile_resources('seahorse-resources',
  'seahorse-nautilus.gresource.xml',
  c_name: 'seahorse',
)

seahorse_tool_sources = [
  'seahorse-notification.c',
  'seahorse-operation.c',
  'seahorse-passphrase.c',
  'seahorse-pgp-operation.c',
  'seahorse-progress.c',
  'seahorse-tool.c',
  'seahorse-tool-files.c',
  'seahorse-tool-progress.c',
  'seahorse-util.c',
  'seahorse-vfs-data.c',
  'seahorse-widget.c',
  marshaller,
]

seahorse_tool_dependencies = [
  glib,
  gio,
  gtk,
  gcr,
  cryptui,
  gpgme,
]

if libnotify_enabled
  seahorse_tool_dependencies += libnotify
endif

seahorse_tool_cflags = [
	'-DLIBCRYPTUI_API_SUBJECT_TO_CHANGE',
	'-DGCR_API_SUBJECT_TO_CHANGE',
]

seahorse_tool = executable('seahorse-tool',
  seahorse_tool_sources,
  dependencies: seahorse_tool_dependencies,
  c_args: seahorse_tool_cflags,
  include_directories: config_h_dir,
  install: true,
)

# Manpage
install_man('seahorse-tool.1')

# The desktop file
desktop_files = [
  'seahorse-pgp-encrypted.desktop',
  'seahorse-pgp-signature.desktop',
  'seahorse-pgp-keys.desktop',
]

foreach desktop_file : desktop_files
  desktop_conf = configuration_data()
  desktop_conf.set('bindir', bindir)
  desktop_conf.set('VERSION', meson.project_version())

  configured_desktop_file = configure_file(
    input: desktop_file + '.in.in',
    output: desktop_file + '.in',
    configuration: desktop_conf,
  )
  i18n.merge_file(
    input: configured_desktop_file,
    output: desktop_file,
    type: 'desktop',
    po_dir: po_dir,
    install: true,
    install_dir: join_paths(datadir, 'applications')
  )
endforeach
