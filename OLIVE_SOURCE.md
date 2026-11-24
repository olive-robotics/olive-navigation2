# Olive Navigation2 / AMCL source release

This source distribution accompanies the nav2_amcl libraries in Olive's ARM64
Robot firmware. Olive adds source-delivery documentation, complete upstream
snapshots and license copies. No upstream implementation file is modified.

## Versions and correspondence

| ROS distribution | Package version | Official upstream commit | Matching installed files | Matching binary log locations |
| --- | --- | --- | --- | --- |
| Humble | 1.1.19 | `bf40e4d5dfdd02d24e05e75f14a770cb9e349be9` | 15 | 49 |
| Jazzy | 1.3.12 | `6be3614013ec586051b86c97b919b293281490fe` | 15 | 51 |

The complete Navigation2 repository is retained because AMCL uses other
Navigation2 packages and their CMake helpers. Other Navigation2 packages retain
their original licenses; including them here does not relicense them as LGPL.
The main tree follows `1.3.12`; both complete release snapshots are in
`source-release/`.

The owner reports that official sources were used without local source changes.
[SOURCE_MANIFEST.json](SOURCE_MANIFEST.json) records the compared files, SHA256
fingerprints and source-location checks. These checks support the selected
source revisions; they are not a byte-identical rebuild of the shipped binaries.
The original build machine's compiler configuration was not recovered.

## License notices

AMCL declares LGPL-2.1-or-later. The repository root LICENSE describes much of
Navigation2 as Apache-2.0; that does not replace AMCL’s per-file LGPL notices.
The original copyright headers and notices are preserved. Full LGPL and GPL
license texts are additionally included in `source-release/LICENSES/`.

## Extract and build

Choose the snapshot for the ROS distribution being used; do not mix Humble and
Jazzy snapshots. `source-release/SHA256SUMS` covers archives and license copies.
For example, for Humble:

```sh
cd source-release
sha256sum -c SHA256SUMS
mkdir -p /tmp/olive-nav-build/src
tar -xzf navigation2-1.1.19.tar.gz -C /tmp/olive-nav-build/src
mv /tmp/olive-nav-build/src/navigation2-1.1.19 /tmp/olive-nav-build/src/navigation2
cd /tmp/olive-nav-build
. /opt/ros/humble/setup.sh
rosdep install --from-paths src --ignore-src --rosdistro humble -r -y
colcon build --packages-up-to nav2_amcl --cmake-args -DCMAKE_BUILD_TYPE=Release -DBUILD_TESTING=OFF
```

For Jazzy, select its archive and source `/opt/ros/jazzy/setup.sh`, and pass
`--rosdistro jazzy` to rosdep. Use a matching target architecture and compatible
ROS dependencies. The original `package.xml` files list dependencies and the
original `CMakeLists.txt` files control compilation and installation. Dependencies
resolved today can differ from the original build environment. No new binary
build or runtime replacement was performed for this source release.

The source-delivery documentation is on main, tagged `olive-navigation2-sources-20261124`.
The exact upstream commits listed above remain available through Git history
and the included source archives.
