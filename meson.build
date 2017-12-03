project('seahorse-nautilus', 'c',
  version: '3.11.92',
  meson_version: '>= 0.42',
  license: 'GPL2+',
)

gnome = import('gnome')
i18n = import('i18n')

# Options
check_compatible_gpg = get_option('check-compatible-gpg')
libnotify_enabled = get_option('libnotify')
nautilus_ext_dir = get_option('nautilus-ext-dir')

# Some useful variables
cc = meson.get_compiler('c')
seahorse_nautilus_prefix = get_option('prefix')
po_dir = join_paths(meson.source_root(), 'po')
datadir = join_paths(seahorse_nautilus_prefix, get_option('datadir'))
bindir = join_paths(seahorse_nautilus_prefix, get_option('bindir'))
localedir = join_paths(seahorse_nautilus_prefix, get_option('localedir'))
uidir = join_paths(datadir, 'seahorse-nautilus', 'ui')
config_h_dir = include_directories('.')

# Dependencies
min_glib_version = '2.10.0'
accepted_gpg_versions= ['1.2.0', '1.4.0', '2.0.0', '2.1.0', '2.2.0' ]
min_gpgme_version = '1.0.0'

libnautilus_extension = dependency('libnautilus-extension', version: '>= 2.12.0')
if nautilus_ext_dir == ''
  nautilus_ext_dir = libnautilus_extension.get_pkgconfig_variable('extensiondir')
endif
message('Nautilus extension dir: "@0@"'.format(nautilus_ext_dir))

glib = dependency('gio-2.0', version: '>= ' + min_glib_version)
gio = dependency('gio-2.0', version: '>= ' + min_glib_version)
gtk = dependency('gtk+-3.0', version: '>= 3.0')
dbus_glib = dependency('dbus-glib-1', version: '>= 0.35')
cryptui = dependency('cryptui-0.0', version: '>= 3.9.90')
gcr = dependency('gcr-3', version: '>= 3.4.0')
if libnotify_enabled
  libnotify = dependency('libnotify', version: '>= 0.3')
endif

gpg_check_version = find_program(join_paths('meson', 'gpg_check_version.py'))
gpg_bin = find_program('gpg2', 'gpg')
gpgme = cc.find_library('gpgme')
gpgme_config = find_program('gpgme-config')
if check_compatible_gpg
  gpg_version_check = run_command([gpg_check_version, gpg_bin.path(), 'false', accepted_gpg_versions ])
  gpg_version = gpg_version_check.stdout()
  message('GnuPG Version: @0@'.format(gpg_version))
  if gpg_version_check.returncode() != 0
    error('Incompatible version of GnuPG. Accepted versions are: @0@'.format(accepted_gpg_versions))
  endif

  gpgme_version_check = run_command([gpg_check_version, gpgme_config.path(), 'true', min_gpgme_version ])
  gpgme_version = gpgme_version_check.stdout()
  message('GPGME version: @0@'.format(gpgme_version))
  if gpgme_version_check.returncode() != 0
    error('Incompatible version of GPGME. Minimal version required is @0@'.format(min_gpgme_version))
  endif
endif

# Configuration
conf = configuration_data()
conf.set_quoted('VERSION', meson.project_version())
conf.set_quoted('PACKAGE', meson.project_name())
conf.set_quoted('PACKAGE_NAME', meson.project_name())
conf.set_quoted('PACKAGE_VERSION', meson.project_version())
conf.set_quoted('PACKAGE_STRING', '@0@ @1@'.format(meson.project_name(), meson.project_version()))
conf.set_quoted('GETTEXT_PACKAGE', meson.project_name())
conf.set_quoted('G_LOG_DOMAIN', meson.project_name())
conf.set_quoted('DATA_DIR', datadir)
conf.set_quoted('LOCALEDIR', localedir)
conf.set_quoted('GNOMELOCALEDIR', localedir)
conf.set_quoted('SEAHORSE_UIDIR', uidir)
conf.set('HAVE_LIBNOTIFY', libnotify_enabled)
config_file = configure_file(
  output: 'config.h',
  configuration: conf,
)

# Post-install scripts
meson.add_install_script(join_paths('meson', 'post_install.py'))

# subdirs
subdir('data')
subdir('tool')
subdir('nautilus-ext')
subdir('po')
