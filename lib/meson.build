# Compiled library

args = ['-DTOML_HEADER_ONLY=0']

lib = library(
	meson.project_name(),
	'toml++'/'toml.cpp',
	cpp_args: args,
	include_directories: include_dir,
	install: not is_subproject,
	version: meson.project_version()
)

tomlplusplus_dep = declare_dependency(
	compile_args: args,
	include_directories: include_dir,
	link_with: lib
)

if not is_subproject
	import('pkgconfig').generate(
		lib,
		description: 'TOML config file parser and serializer for C++',
		extra_cflags: args,
		url: 'https://marzer.github.io/tomlplusplus'
	)
endif

# cmake
if get_option('generate_cmake_config') and not is_subproject
	cmake = import('cmake')
	cmake.write_basic_package_version_file(
		name: meson.project_name(),
		version: meson.project_version(),
	)

	lib_name = lib.full_path().split('/')[-1] # last component is the file name

	cmake_conf = configuration_data({
		'compile_library': get_option('compile_library'),
		'libdir': get_option('libdir'),
		'lib_name': lib_name
	})

	cmake.configure_package_config_file(
		name: meson.project_name(),
		input: '..'/'cmake'/'tomlplusplus.cmake.in',
		configuration: cmake_conf
	)
endif
