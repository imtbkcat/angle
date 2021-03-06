vars = {
  'android_git': 'https://android.googlesource.com',
  'chromium_git': 'https://chromium.googlesource.com',
}

deps = {

  'build':
    Var('chromium_git') + '/chromium/src/build.git' + '@' + 'cdd940cfcab2d20be1e6fd49e3580e531a5e7305',

  'buildtools':
    Var('chromium_git') + '/chromium/buildtools.git' + '@' + 'e043d81e9185a2445fa3ec3fc34a4f69b58d4969',

  'testing':
    Var('chromium_git') + '/chromium/src/testing' + '@' + 'd57c35d68320b906c43ad3f0ea5d84da3d06f45d',

  # Cherry is a dEQP management GUI written in Go. We use it for viewing test results.
  'third_party/cherry':
    Var('android_git') + '/platform/external/cherry' + '@' + 'd2e26b4d864ec2a6757e7f1174e464949ca5bf73',

  'third_party/deqp/src':
    Var('android_git') + '/platform/external/deqp' + '@' + '455d82c60b096e7bd83b6a2f5ed70c61e4bfa759',

  'third_party/glslang-angle/src':
    Var('android_git') + '/platform/external/shaderc/glslang' + '@' + '1e275c8486325aaab34734ad9a650c0121c5efdb',

  'third_party/googletest/src':
    Var('chromium_git') + '/external/github.com/google/googletest.git' + '@' + '7f8fefabedf2965980585be8c2bff97458f28e0b',

  'third_party/libpng/src':
    Var('android_git') + '/platform/external/libpng' + '@' + '094e181e79a3d6c23fd005679025058b7df1ad6c',

  'third_party/spirv-headers/src':
    Var('android_git') + '/platform/external/shaderc/spirv-headers' + '@' + 'c470b68225a04965bf87d35e143ae92f831e8110',

  'third_party/spirv-tools-angle/src':
    Var('android_git') + '/platform/external/shaderc/spirv-tools' + '@' + '68c5f0436f1d4f1f137e608780190865d0b193ca',

  'third_party/vulkan-validation-layers/src':
    Var('android_git') + '/platform/external/vulkan-validation-layers' + '@' + 'f47c534fee2f26f6b783209d56e0ade48e30eb8d',

  'third_party/zlib':
    Var('chromium_git') + '/chromium/src/third_party/zlib' + '@' + '24ab14872e8e068ba08cc31cc3d43bcc6d5cb832',

  'tools/clang':
    Var('chromium_git') + '/chromium/src/tools/clang.git' + '@' + 'dce401419c4281e2aad72a9bafb885a9fb9aec59',

  'tools/gyp':
    Var('chromium_git') + '/external/gyp' + '@' + 'c6f471687407bf28ddfc63f1a8f47aeb7bf54edc',

}

hooks = [
  # Pull clang-format binaries using checked-in hashes.
  {
    'name': 'clang_format_win',
    'pattern': '.',
    'action': [ 'download_from_google_storage',
                '--no_resume',
                '--platform=win32',
                '--no_auth',
                '--bucket', 'chromium-clang-format',
                '-s', 'buildtools/win/clang-format.exe.sha1',
    ],
  },
  {
    'name': 'clang_format_mac',
    'pattern': '.',
    'action': [ 'download_from_google_storage',
                '--no_resume',
                '--platform=darwin',
                '--no_auth',
                '--bucket', 'chromium-clang-format',
                '-s', 'buildtools/mac/clang-format.sha1',
    ],
  },
  {
    'name': 'clang_format_linux',
    'pattern': '.',
    'action': [ 'download_from_google_storage',
                '--no_resume',
                '--platform=linux*',
                '--no_auth',
                '--bucket', 'chromium-clang-format',
                '-s', 'buildtools/linux64/clang-format.sha1',
    ],
  },
  # Pull GN binaries using checked-in hashes.
  {
    'name': 'gn_win',
    'pattern': '.',
    'action': [ 'download_from_google_storage',
                '--no_resume',
                '--platform=win32',
                '--no_auth',
                '--bucket', 'chromium-gn',
                '-s', 'buildtools/win/gn.exe.sha1',
    ],
  },
  {
    'name': 'gn_mac',
    'pattern': '.',
    'action': [ 'download_from_google_storage',
                '--no_resume',
                '--platform=darwin',
                '--no_auth',
                '--bucket', 'chromium-gn',
                '-s', 'buildtools/mac/gn.sha1',
    ],
  },
  {
    'name': 'gn_linux64',
    'pattern': '.',
    'action': [ 'download_from_google_storage',
                '--no_resume',
                '--platform=linux*',
                '--no_auth',
                '--bucket', 'chromium-gn',
                '-s', 'buildtools/linux64/gn.sha1',
    ],
  },
  {
    # Pull clang if needed or requested via GYP_DEFINES.
    # Note: On Win, this should run after win_toolchain, as it may use it.
    'name': 'clang',
    'pattern': '.',
    'action': ['python', 'tools/clang/scripts/update.py', '--if-needed'],
  },
  {
    # A change to a .gyp, .gypi, or to GYP itself should run the generator.
    'pattern': '.',
    'action': ['python', 'gyp/gyp_angle'],
  },
]

recursedeps = [
  # buildtools provides clang_format.
  'buildtools',
]
