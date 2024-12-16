# Building

For most users, we recommend importing and building through Android Studio.

## Build variants

There are the following build variants

```
universal (all architectures)
arm64 (arm64-v8a)
uncommonabi (armeabi-v7a, x86, x86_64)
x86_64
```

**For most users, the `universal` variant is sufficient.** The other build variants may reduce file size, however at the
cost of compatibility.

## Building with FFmpeg binaries

By default, we ship a prebuilt library (`/app/prebuilt/ffMetadataEx.arr`), and you *DO NOT* need to care about this.
However, should you choose to opt for self built libraries and/or work on the extractor itself, keep reading:

1. First you will need to setup the [Android NDK](https://developer.android.com/studio/projects/install-ndk)

2. We use FFMpeg to extract metadata from local files. The FFMpeg binaries must be resolved in one of two ways:

    - a) Build libraries yourself. Clone [ffmpeg-android-maker](https://github.com/Javernaut/ffmpeg-android-maker) into
      `/ffMetadataEx/src/main/cpp/ffmpeg-android-maker`, run the build script. Note: It may be helpful to modify the
      FFmpeg build script disable uneeded FFmpeg fetaures to reduce app size,
      see [here](https://github.com/mikooomich/ffmpeg-android-maker/blob/master/scripts/ffmpeg/build.sh) for an example.

    - b) Use prebuilt FFmpeg libraries.
      Clone [prebuilt ffmpeg-android-maker](https://github.com/mikooomich/ffmpeg-android-maker-prebuilt) into
      `/ffMetadataEx/src/main/cpp/ffmpeg-android-maker`.

3. Modify `app/build.gradle.kts` and `settings.gradle.kts` to switch to the self built version, with the instructions
   being in both of the files.

4. Start the build are you normally would.

<br/><br/>

# Contributing to OuterTune

## Submitting a pull request
To make eveyone's life easier, there are a set of guidlines that are to be followed when submitting pull requests.

- One pull request for one feature/issue, please refrain from tackling many features/issues in one pull request
- Write a descriptive title and a meaningful description
- Upload images/video for any UI changes
- In the event of merge conflicts, you may be required to rebase onto the current `dev` branch
- **You are required to build and test the app before submitting a pull request**

## Commiting guidelines
- Prefix commits with tags, and provide descriptions if necessary. These are generally done in format:
  `tag: commit_name`. [Example](https://github.com/DD3Boh/OuterTune/commit/798e8366227dd2cc38355224c733dbf7e8ffcee0)
    - A list of tags commonly used is provided below
- Commit descriptions are not required, but highly recommended
- When porting/cherry-picking/stealing from other repositories or sources:
    - Maintain
      authorship. [Example](https://github.com/DD3Boh/OuterTune/commit/b0dc59682190b41f0200e9df5174322acaa3d40d)
    - If this is not possible please provide the source in the commit
      description. [Example](https://github.com/DD3Boh/OuterTune/pull/59/commits/e40325dd86ac2c30347cfd4f9e92bbf15a0d0c82)
- Do not merge `dev` into your branch
    - Instead, please rebase over dev
- Merge conflicts
    - As per the previous point, please rebase and conflicts are to be resolve in the commits themselves
    - We may ask you to rebase your PR if merge conflicts are an issue when merging
- If database schema changes are required, please state clearly if a version increment is required. Additional details
  are in the `Database schema changes` section
- For multi-part commits where all parts are required for functionality, use
  `[1/2], [2/2], etc`. [See example](https://github.com/DD3Boh/OuterTune/pull/59/commits)

### Tags

| Tag (General) | Description                                                                                         |
|---------------|-----------------------------------------------------------------------------------------------------|
| github        | Github facing configs, ex. build scripts, templates, etc.                                           |
| gradle        | Dependency/library updates                                                                          |
| readme        | Readme changes                                                                                      |
| translations  | Translations                                                                                        |
| fixup         | Amendments to certain commits. this is generally done in the format `fixup: <old commit name here>` |

| Tag (ui)    | Description                                                                        |
|-------------|------------------------------------------------------------------------------------|
| ui          | User interface                                                                     |
| multiselect | Multi-select of songs/items in library                                             |
| library     | Library general components. Use the specific ones below if it is a specific change |
| artist      | Playlist screens & components                                                      |
| album       | Album screens & components                                                         |
| playlist    | Playlist screens & components                                                      |
| songs       | Song screens & components                                                          |

| Tag (Playback) | Description               |
|----------------|---------------------------|
| player         | Music playback components | 
| multiqueue     | Queue components          |

| Tag (Features) | Description                 |
|----------------|-----------------------------|
| sync           | YouTube Music sync features |
| downloads      | Offline song downloads      |
| innertube      | Innertube module            |

| Tag (Misc)    | Description                                                      |
|---------------|------------------------------------------------------------------|
| `<file name>` | Changes for one single file, that to not fit into any other tags |
| app           | General changes, or anything that does not fit any other tags    |

- Please use a tag if it already exists, however, if you are developing a new major feature, you are free to assign your
  own appropriate tag
- Tags can be stacked. For example: `ui: library: Something something`

## Database schema changes

- Clearly state if a database version increment is required
- You are require to make sure migration works from the previous database version
- Commits modifying the database version should be all be contained in that single commit
    - The generate json JSON, Entity classes, migration conflict resolution, etc.

## Translations
Follow the [instructions](https://developer.android.com/guide/topics/resources/localization) to add tranlation strings, and then
create a pull request. **You are also required to build the app beforehand** and make sure there is no error
before you create a pull request.