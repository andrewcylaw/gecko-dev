:mod:`mozproxy` --- Provides an HTTP proxy
==========================================

Mozproxy let you launch an HTTP proxy when we need to run tests against
third-part websites in a reliable and reproducible way.

Mozproxy provides an interface to a proxy software, and the currently
supported backend is **mitmproxy** for Desktop and Android.

Mozproxy is used by Raptor to run performance test without having to interact
with the real web site.

Mozproxy provide a function that returns a playback class. The usage pattern is
::

   from mozproxy import get_playback

   config = {'playback_tool': 'mitmproxy'}
   pb = get_playback(config)
   pb.start()
   try:
     # do your test
   finally:
     pb.stop()

**config** is a dict with the following options:

- **playback_tool**: name of the backend. can be "mitmproxy", "mitmproxy-android"
- **playback_recordings**: list of recording files
- **playback_binary_manifest**: tooltool manifests for the proxy backend binary
- **playback_pageset_manifest**: tooltool manifest for the pagesets archive
- **binary**: path of the browser binary
- **obj_path**: build dir
- **platform**: platform name (provided by mozinfo.os)
- **run_local**: if True, the test is running locally.
- **custom_script**: name of the mitm custom script (-s option)
- **app**: tested app. Can be "firefox",  "geckoview", "refbrow", "fenix" or  "firefox"
- **host**: hostname for the policies.json file
- **local_profile_dir**: profile dir


Supported environment variables:

- **MOZ_UPLOAD_DIR**: upload directory path
- **GECKO_HEAD_REPOSITORY**: used to find the certutils binary path from the CI
- **GECKO_HEAD_REV**: used to find the certutils binary path frmo the CI
- **HOSTUTILS_MANIFEST_PATH**: used to find the certutils binary path from the CI
