load('//:subdir_glob.bzl', 'subdir_glob')

cxx_library(
  name = 'textinput',
  header_namespace = '',
  exported_headers = subdir_glob([
    ('', 'textinput/**/*.h'),
  ]),
  srcs = glob([
    'textinput/**/*.cpp',
  ]),
  visibility = [
    'PUBLIC',
  ],
)
