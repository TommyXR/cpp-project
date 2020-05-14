project('{0}', 'cpp',
    default_options: [
        'cpp_std=c++2a',
    ]
)


srcs = [files('src/main.cpp')]
deps = []
include_dirs = []
link_args = []


# OS specific things
if host_machine.system() == 'windows'
    link_args += '--static'

elif host_machine.system() == 'linux'
    # May need -ldl for C libraries
endif


# Build types
if get_option('buildtype') == 'debug'
    add_project_arguments('-D__DEBUG_BUILD', language: 'cpp')

elif get_option('buildtype') == 'release'

endif



# Main program
executable('{0}',
    sources: srcs,
    include_directories: include_dirs,
    dependencies: deps,
    link_args: link_args
)

# Tidying support, just run `ninja tidy`
clangtidy = find_program('clang-tidy', required: false)
if clangtidy.found()
    run_target('tidy',
      command: [
        clangtidy,
        '-p', meson.build_root()
        ] + srcs)
endif
